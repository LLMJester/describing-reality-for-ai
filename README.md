# Describing Reality for AI

*Which way of writing a system down helps a small AI reason about it, and why*

**Read the white paper:** https://llmjester.github.io/describing-reality-for-ai/ (also as a PDF in `docs/`).

## The result in brief

A small model (GPT-6 Luna) writes a system down as notes, then answers questions from its notes alone. Fifteen note
formats sat one exam. **Short facts** (five headings, one short fact per line) won: **65% right on 720 sealed
questions no AI had seen, against 49% for plain prose notes** (+0.163, 95% range 0.140 to 0.186). Twenty-five new
versions of its parts were then tested in two rounds; none beat it, and adding rules or structure made it worse. On
messy real-world documents no format did much better than prose. 43,995 pre-registered test runs in all.

## What is here

| Folder | What it holds |
| --- | --- |
| `docs/` | The paper: the designed web edition (served by GitHub Pages) and its PDF |
| `results/` | The run's results: `episodes.csv` (one row per scored test run: stage, design, item id, system size, score, whether the notes passed their check, tokens, seconds), `designs.json` (every design's genome), `new_parts/` (what the designer AI wrote, and the summary it was given), `analysis.json` (every pre-registered test, effect, range and verdict), `events.json` (the run's log), `COUNTS.json` |
| `harness/` | The code that ran the experiment, with the pre-registration, the decision log and the lock (see `harness/README.md`) |

The winning format, with a copy-paste prompt card, is in Appendix A of the paper.

## What is not here

No item text, questions, answer keys, notes or transcripts. Generated items can be rebuilt from their seeds with the
code in `harness/`; the 500 hand-written items are held back for future runs (the factory that made them is
included). The first sealed set was retired unused after a design change (V3-058); its 1,435 runs are not exported.
