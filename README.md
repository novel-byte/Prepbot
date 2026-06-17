# Prepbot

An exam preparation platform that studies your resources and past papers, then
predicts what the next exam will ask.

**Status: not yet implemented.** This repository holds the design and the
intended behaviour. The code is not written yet.

## The problem

Preparing for an exam from a pile of past papers is a lot of work done by
hand. You read each paper, notice which topics keep coming up, work out
which questions were asked in what style, and try to guess what is coming
next.

That analysis is mechanical, and it is exactly the kind of thing that is
tedious enough that people skip it — and skip it is precisely what the
person doing the exam has also done, to the person marking it.

Prepbot does the analysis instead. You give it your resources and your past
exams, and it tells you what to revise.

## What it does

**Reads what you have.** Past papers, notes, syllabuses, handouts — whatever
you have been studying from. PDFs, Markdown, text.

**Works out the syllabus.** The topics that come up, how often each one
appears, and how the emphasis shifts between papers. A topic that appeared
in every paper is a topic that is certain to appear again.

**Notices the question patterns.** How questions are phrased for a given
topic. Past papers repeat themselves in structure even when the numbers
change, and the way a question is set often tells you what is being tested
and how deeply.

**Predicts the next paper.** Questions generated for the topics and patterns
it found, ranked by how likely each is to appear. Not the actual paper — a
well-founded guess at what to spend your remaining time on.

## How the analysis works

**Topic extraction.** Concepts are pulled from the text and grouped into
topics, so that "photosynthesis" and "light-dependent reactions" end up as
one topic rather than two. The grouping is learned from the corpus rather
than from a fixed list, because the vocabulary of an exam is not the
vocabulary of a textbook.

**Weighting.** A topic's weight comes from how often it appears across
*different* papers, not how often it appears in total. One paper that
repeats a topic five times should not outweigh four papers that each mention
it once. Recency counts too, but less heavily, because a syllabus does not
change as quickly as a revision schedule does.

**Pattern matching.** Questions are compared on their structure rather than
their wording: how many parts, how many marks, what they ask for, how much
reading they need. Two questions on the same topic with the same structure
are a pattern, whatever the numbers in them are.

**Prediction.** The topics and patterns found are combined into a ranked list
of what to expect. Each prediction carries the reasoning — which papers it
came from, and why it ranks where it does — so a prediction can be argued
with rather than merely trusted.

## The interface

**Upload.** Drop in past papers and notes. Prepbot reads them and shows what
it found: the topics, their weights, and a summary of each paper.

**Study.** A ranked list of predicted questions, each with the topic it
comes from and the reasoning behind it.

**Revise.** A view of the topics, ordered by how much they are worth, with
the questions that have appeared on each before. This is the list to work
through.

**Practice.** Predicted questions, answered under exam conditions — no
notes, a timer, and the marks allocated the way they would be. Afterwards,
the gaps are pointed out.

## What it is not

- **Not a cheating tool.** It studies the papers you were given. It does not
  reach for a live paper, and it will not help you with an exam that is
  happening right now.
- **Not a language model wrapper.** The interesting work is the analysis:
  extracting topics from a corpus, weighting them across papers, and finding
  structural patterns. A language model may help with some of it, but it is
  not the design.
- **Not a promise of accuracy.** A prediction is a well-supported guess about
  a syllabus, and past papers are evidence rather than a guarantee. The
  ranking is the useful part; treating the top of it as certain is not.

## What it would be written in

Python. The analysis is a pile of text processing and statistics, and the
libraries for that are good.

## Licence

MIT.
