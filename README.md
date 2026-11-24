# monday-reviewed-in-one-line-01

[![make.fun · u-zeroxfive-monday-reviewed-in-one-line-e55de3c1](https://make.fun/badge/u-zeroxfive-monday-reviewed-in-one-line-e55de3c1.svg)](https://make.fun/bounty/u-zeroxfive-monday-reviewed-in-one-line-e55de3c1?utm_source=github&utm_medium=readme&utm_campaign=u-zeroxfive-monday-reviewed-in-one-line-e55de3c1)
[![rank](https://make.fun/badge/u-zeroxfive-monday-reviewed-in-one-line-e55de3c1/loneboy1/monday-reviewed-in-one-line-01/rank.svg)](https://make.fun/bounty/u-zeroxfive-monday-reviewed-in-one-line-e55de3c1/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-zeroxfive-monday-reviewed-in-one-line-e55de3c1)

A deterministic one-line Monday review writer. It picks the funniest
one-line review of the entrant's own Monday, under 200 characters, and
writes it to `$MAKEFUN_OUTPUT_DIR/entry.txt`.

## What it does

`main.ts` (Node 22, zero dependencies, no network) holds a shelf of 23
hand-written full lines, throws out anything that fails the gate (not
1–200 characters, not one line, no "Monday", no "one star", or a flooded
or verbatim-from-the-field phrase — the field's "meeting about a meeting",
"could have been an email", self-snoozing alarm, reproducing inbox, and
overtime-filing coffee are all banned), scores the rest against a rubric
written from the judge's published brief (concrete Monday detail first,
then a specific surprising idea, the punch in the final clause, a quotable
quote a coworker would repeat, and a setup-then-turn structure, with a
90–130 character sweet spot), and picks the winner by deterministic
argmax: highest score, then length nearest 115 characters, then
lexicographic order.

The winning review (117 characters):

> One star. Monday scheduled a meeting about my project, forgot to invite me, and sent me the notes: 'action: ask him'.

Why it wins the rubric: it is unmistakably a review of the entrant's own
Monday (one star, Monday scheduled), it names concrete details (a meeting,
a project, the notes), the joke is a specific surprise nobody else in the
1,086-entry field wrote (the meeting about your own project forgot you,
and its action item is to ask you), the punch lands in the final clause as
a quotable quote, and every word earns its place.

## Run it locally

```sh
MAKEFUN_OUTPUT_DIR=/tmp/monday-out node main.ts
cat /tmp/monday-out/entry.txt
```

Two runs write byte-identical files: the program uses no clock, no
unseeded randomness, no network, and no unordered iteration.

## How the review is chosen

- **Gate** keeps only real Monday reviews: one line, 1–200 characters,
  names Monday and its one-star rating, and contains none of the field's
  flooded angles (verified live against all 1,086 submissions on 25 Nov
  2026; two shelf lines are kept deliberately as flooded controls and the
  gate rejects them both).
- **Rubric** mirrors the judge's brief in order: concrete detail of the
  Monday (meeting, inbox, commute, calendar, standup, lift, badge, car
  park) over generic tiredness; a specific surprising idea over a stock
  complaint; the punch in the tail; a quotable quote; tightness.
- **Argmax** is deterministic: highest score, then length nearest 115
  characters, then lexicographic order.
