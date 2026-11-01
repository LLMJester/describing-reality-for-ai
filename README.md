# Describing Reality for AI

*Which way of writing a system down helps a small AI reason about it, and why*

**Read the white paper:** https://llmjester.github.io/describing-reality-for-ai/ (also as a PDF in `docs/`).

## The result in brief

A small model (GPT-6 Luna) writes a system down as notes, then answers questions from its notes alone. Fifteen note
formats sat one exam. **Short facts** (five headings, one short fact per line) won: **65% right on 720 sealed
questions no AI had seen, against 49% for plain prose notes** (+0.163, 95% [cluster-bootstrap][cluster] range 0.140
to 0.186). Twenty-five new versions of its parts were then tested in two rounds; none beat it, and adding rules or
structure made it worse. On messy real-world documents no format did much better than prose. 43,995
[pre-registered][prereg] test runs in all.

The methods behind each verdict ([Hsu's comparisons with the best][hsu], [Holm's correction][holm], the [full
factorial][factorial], the [winner's curse][curse], [fixed-sequence gatekeeping][gatekeeping]) are explained in
the paper; each name above links to its source.

[prereg]: https://doi.org/10.1073/pnas.1708274114
[cluster]: https://doi.org/10.1111/j.1467-9868.2007.00593.x
[hsu]: https://doi.org/10.1214/aos/1176346732
[holm]: https://www.jstor.org/stable/4615733
[factorial]: https://www.itl.nist.gov/div898/handbook/pri/section3/pri3331.htm
[curse]: https://doi.org/10.1097/EDE.0b013e31818131e7
[gatekeeping]: https://www.fda.gov/media/162416/download

## Two repositories

| Repository | What it is for |
| --- | --- |
| **describing-reality-for-ai** (this one) | The details of this run: the paper, the results and the rules it was run under |
| **[reality-engine](https://github.com/LLMJester/reality-engine)** | The engine, to run the same method on your own problem. This run is its first worked example, with its code |

## What is here

| Folder | What it holds |
| --- | --- |
| `docs/` | The paper: the designed web edition (served by GitHub Pages) and its PDF |
| `results/` | The run's results: `episodes.csv` (one row per scored test run: stage, design, item id, system size, score, whether the notes passed their check, tokens, seconds), `designs.json` (every design's genome), `new_parts/` (what the designer AI wrote, and the summary it was given), `analysis.json` (every pre-registered test, effect, range and verdict), `events.json` (the run's log), `COUNTS.json` |
| `rules/` | The rules the run was locked to before its first result: the pre-registration (`PREREG.md`), the dated decision log (`DECISIONS.md`), the run 5 design documents and the lock (`PREREG.LOCK`, the hashes of the code and rules) |

The winning format, with a copy-paste prompt card, is in Appendix A of the paper.

## What is not here

No item text, questions, answer keys, notes or transcripts, and not the item generator: with it, anyone could
rebuild the answer keys of the sealed sets. The 500 hand-written items are held back for future runs. The first
sealed set was retired unused after a design change (V3-058); its 1,435 runs are not exported.
