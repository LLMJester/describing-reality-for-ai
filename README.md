# Describing Reality for AI

*Which way of writing a system down helps a small AI reason about it, and why*

**Read the white paper:** https://therealityengine.ca/paper/ ([download the PDF](https://therealityengine.ca/paper/Describing-Reality-for-AI.pdf)). A mirror is in `docs/`, served by GitHub Pages.

## The result in brief

A small model (GPT-6 Luna) writes a system down as notes, then answers questions from its notes alone. Fifteen note
formats sat one exam. **Short facts** (five headings, one short fact per line) won: **65% of questions right on 720
sealed items no AI had seen, against 49% for plain prose notes** (+0.163, 95% [cluster-bootstrap][cluster] range
0.140 to 0.186). Twenty-five new versions of its parts were then tested in two rounds; none beat it, and adding rules
or structure made it worse. On messy realistic documents (written by AI in the style of operations documents) no format did much better than
prose. 43,995 test runs in all, each under rules locked before it ran ([pre-registration][prereg]); 1,435 of them, on
a retired sealed set, are not exported, so `episodes.csv` holds 42,560.

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
| `docs/` | A mirror of the paper (served by GitHub Pages) and its PDF; the main copy is at https://therealityengine.ca/paper/ |
| `results/` | The run's results: `episodes.csv` (one row per scored test run: stage, design, item id, system size, score, whether the notes passed their format check, blank for designs with no check; `item_set = hand_written` is the 500 realistic documents, a name kept from the run's code, tokens, seconds), `designs.json` (every design's genome), `new_parts/` (what the designer AI wrote, and the summary it was given), `analysis.json` (every pre-registered test, effect, range and verdict), `events.json` (the run's log), `COUNTS.json` |
| `rules/` | The rules the run was locked to, each before it was used (stages 3 to 5 were added and locked after stage 2, V3-058): the pre-registration (`PREREG.md`), the dated decision log (`DECISIONS.md`), the run 5 design documents and the lock (`PREREG.LOCK`, the hashes of the code and rules) |

The winning format, with a copy-paste prompt card, is in Appendix A of the paper.

## What is not here

No item text, questions, answer keys, notes or transcripts, and not the item generator: with it, anyone could
rebuild the answer keys of the sealed sets. The 500 realistic documents are held back for future runs. The first
sealed set was retired after a design change and never analyzed (V3-058); its 1,435 runs are not exported.
