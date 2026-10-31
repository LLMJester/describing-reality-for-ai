# Describing Reality for AI: the run 5 harness

This folder is the code that ran run 5 of the Discovery Programme, the experiment reported in the white paper
"Describing Reality for AI". It is a snapshot with no git history, built by `rpp-v3/scripts/build_release.py`.
`MANIFEST.json` lists every file with its SHA-256 and the commits it came from.

## What the experiment does

A small model (GPT-6 Luna) reads a long description of a system and writes notes without seeing the questions. A fresh
session then answers the questions from the notes alone. Run 5 compares note formats on one shared exam:

1. **Stage 1.** 15 founding formats and a no-notes baseline answer 480 generated items (120 systems at sizes
   k = 1, 2, 4, 8) and 500 hand-written-style items. The winner is the highest mean on the generated items.
2. **Stage 2 prep.** Claude Opus writes a new version of each of the winner's five parts (notes layout, fact writing,
   answering, worked example, thinking budget) from the recipe and a firewalled summary of stage 1 scores. Code checks
   them, a person approves them.
3. **Stage 2.** All 2^5 = 32 combinations of old and new parts answer the same 480 items. Stages 1 and 2 are the deep
   scan. A part is kept only if its effect is clearly positive (Holm) and the new design then wins head to head.
4. **Stages 3 to 5 (V3-058).** Opus writes 20 new versions (4 per part) from a summary of the last stage; a person
   approves them; each is screened alone on 320 fresh items, and the best per part (if it leads by 0.015 or more, at
   most 4) is tested in every mix on 480 more. The stages stop when nothing beats the current best.
5. **Final check.** The final design, the control, the best founder on hand-written items and the runner-up answer 720
   fresh sealed items, opened once, compared in that fixed order.

The rules are in `rpp-v3/PREREG.md` (run 5 section), `rpp-v3/docs/RUN5_DESIGN.md` and `rpp-v3/docs/RUN5_STAGES_DESIGN.md`.
Every change is in `rpp-v3/DECISIONS.md` (V3-042 to V3-058). `rpp-v3/state/PREREG.LOCK` holds the hashes the run was locked with;
`python -m v3.prereg verify` checks them.

## Layout

| Folder | What it holds |
| --- | --- |
| `rpp-v3/v3/` | The experiment: `run5.py` (engine), `analysis5.py` (all statistics), `plus5.py` (stage 2 parts), `run5_sets.py` (item sets), `episode.py` (two-phase run), `sandbox.py` (Docker), `hand5/` (hand-written item factory), `dashboard5/` (live dashboard) |
| `rpp-v3/tests/` | The test suite (about 400 tests; models are faked) |
| `rpp-v3/sandbox/` | The Docker image for model-written code |
| `rpp-core/` | The read-only parts of the earlier framework that run 5 uses: item generators (`discovery/world`), the model-call layer, the judge and the representation tools (`tournament/arms`). Only the files run 5 opens are included; no data sets. |

## Running it

Requirements (versions the run used): Python 3.12 with numpy 2.5; Docker 29 (the sandbox image builds itself);
the Codex CLI 0.163 signed in to a ChatGPT plan with GPT-6 Luna; the Claude Code CLI 2.1 signed in to a Claude plan
(Opus); an OpenRouter key for the judge, read from the `OPENROUTER_API_KEY` environment variable or
`~/.rpp-core/secrets.env`. Keep `rpp-v3` and `rpp-core` side by side (the config's `v2_root` is `../rpp-core`).

```
cd rpp-v3
python -m pytest -q                 # the test suite, no model calls
python -m v3.prereg verify          # the lock: "lock intact" means the code is what ran
python -m v3.run5 mini              # the end-to-end check on pilot items (about 120 runs; never in results)
python -m v3.run5 loop              # the real run (refuses unless the lock verifies)
python -m v3.dashboard5.server5 --port 8766 --mode real
```

`state/PAUSE` stops new runs (running ones finish). The run resumes from its records after a restart.

## What is not here

- Git history of the working repositories (it holds held-out material).
- Run records, transcripts, usage logs and credentials.
- The earlier framework's data sets and gold files.
- The 500 hand-written items, unless this build says `hand_written_items_included: true` in `MANIFEST.json`. They
  can be held back for future runs; the factory that made them (`v3/hand5/`) is included.

Generated items, including the sealed set, are rebuilt from their seeds by `v3/run5_sets.py`.
