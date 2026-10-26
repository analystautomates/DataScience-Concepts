---
title: "Precision"
section: model-evaluation
order: 2
status: written
blurb: "How many flagged cases were real."
---

Precision answers one question: **when the model raises its hand, how
often is it right?**

```
precision = true positives / (true positives + false positives)
```

It reads a single column of the
[confusion matrix]({{ '/learn/confusion-matrix/' | relative_url }}) — the
one containing everybody the model flagged.

<figure><svg viewBox="0 0 480 265" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="The same confusion matrix with the two 'model said churn' cells highlighted"><text class="dg-strong" x="225" y="30" text-anchor="middle">Model said churn</text><text class="dg-strong" x="385" y="30" text-anchor="middle">Model said stay</text><text class="dg-strong" x="140" y="106" text-anchor="end">Actually churned</text><text class="dg-strong" x="140" y="202" text-anchor="end">Actually stayed</text><rect class="dg-hi" x="150" y="58" width="150" height="86" rx="4"/><rect class="dg-cell" x="150" y="58" width="150" height="86" rx="4"/><text class="dg-num" x="164" y="90" text-anchor="start">75</text><text class="dg-numlab" x="164" y="110" text-anchor="start">True positive</text><text class="dg-numlab" x="164" y="126" text-anchor="start">flagged, and they left</text><rect class="dg-cell" x="310" y="58" width="150" height="86" rx="4"/><text class="dg-num" x="324" y="90" text-anchor="start">33</text><text class="dg-numlab" x="324" y="110" text-anchor="start">False negative</text><text class="dg-numlab" x="324" y="126" text-anchor="start">missed, and they left</text><rect class="dg-hi" x="150" y="154" width="150" height="86" rx="4"/><rect class="dg-cell" x="150" y="154" width="150" height="86" rx="4"/><text class="dg-num" x="164" y="186" text-anchor="start">53</text><text class="dg-numlab" x="164" y="206" text-anchor="start">False positive</text><text class="dg-numlab" x="164" y="222" text-anchor="start">flagged, but they stayed</text><rect class="dg-cell" x="310" y="154" width="150" height="86" rx="4"/><text class="dg-num" x="324" y="186" text-anchor="start">839</text><text class="dg-numlab" x="324" y="206" text-anchor="start">True negative</text><text class="dg-numlab" x="324" y="222" text-anchor="start">not flagged, they stayed</text></svg><figcaption>Precision reads the left-hand column: of everyone the model flagged, what share actually churned. The false negatives sitting outside that column are invisible to it.</figcaption></figure>

In this run: 128 flagged, 75 of them genuinely churned. Precision is
**59%**. The other 53 were people the model worried about who were
never going anywhere.

## What it's for

Precision is the metric you care about when **acting on a prediction is
expensive or annoying**.

- A spam filter with poor precision puts real mail in the spam folder.
- A fraud system with poor precision freezes cards of people buying
  groceries.
- A retention campaign with poor precision discounts customers who were
  happily going to renew anyway.

In each case the cost lands on someone who did nothing wrong, which is
why these are the systems where precision gets scrutinised hardest.

## The thing precision cannot see

Look at the diagram again. The 33 false negatives — customers who churned
and were never flagged — sit outside the highlighted column entirely.
They have no effect on precision whatsoever.

That's exploitable. Flag only the single customer the model is most
certain about and precision is near-perfect, while the business loses
almost everyone. Precision on its own is never the answer; it's half of a
pair with [recall]({{ '/learn/recall/' | relative_url }}).

## Getting it

```python
from sklearn.metrics import precision_score

precision_score(y_test, y_pred)                  # for the positive class
precision_score(y_test, y_pred, average=None)    # one per class
```

## Turning the dial

Precision is not fixed. Raise the
[classification]({{ '/learn/classification/' | relative_url }}) threshold
and you only flag the cases the model is surest about, so precision
climbs:

| Threshold | Precision | Recall | Flagged |
|---|---|---|---|
| 0.3 | 26% | 93% | 383 |
| 0.5 | 59% | 69% | 128 |
| 0.7 | 92% | 33% | 39 |

Same model throughout. No retraining. Just a number you chose.

## Where I got stuck

**Hearing "precision" the way a scientist does.** In everyday use,
precision means repeatable and exact. Here it means something narrower —
the hit rate among your flagged cases, and nothing else.

**Quoting it without the base rate.** 59% precision sounds middling
until you notice only 11% of customers churn at all. Against that,
guessing at random would be right about 11% of the time, so the
model is roughly 5.4 times better than chance. The raw percentage means
very little until you know what the floor is.
