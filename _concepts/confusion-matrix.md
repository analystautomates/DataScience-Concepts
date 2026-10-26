---
title: "Confusion Matrix"
section: model-evaluation
order: 5
status: written
blurb: "The four ways a prediction can land."
---

The confusion matrix isn't a metric. It's the table that every other
classification metric is calculated from, which is why I'm writing it up
before [precision]({{ '/learn/precision/' | relative_url }}) and
[recall]({{ '/learn/recall/' | relative_url }}) rather than after.

A prediction can land in exactly four places. That's the whole idea.

<figure><svg viewBox="0 0 480 265" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="A two by two confusion matrix showing true positives, false positives, false negatives and true negatives"><text class="dg-strong" x="225" y="30" text-anchor="middle">Model said churn</text><text class="dg-strong" x="385" y="30" text-anchor="middle">Model said stay</text><text class="dg-strong" x="140" y="106" text-anchor="end">Actually churned</text><text class="dg-strong" x="140" y="202" text-anchor="end">Actually stayed</text><rect class="dg-cell" x="150" y="58" width="150" height="86" rx="4"/><text class="dg-num" x="164" y="90" text-anchor="start">75</text><text class="dg-numlab" x="164" y="110" text-anchor="start">True positive</text><text class="dg-numlab" x="164" y="126" text-anchor="start">flagged, and they left</text><rect class="dg-cell" x="310" y="58" width="150" height="86" rx="4"/><text class="dg-num" x="324" y="90" text-anchor="start">33</text><text class="dg-numlab" x="324" y="110" text-anchor="start">False negative</text><text class="dg-numlab" x="324" y="126" text-anchor="start">missed, and they left</text><rect class="dg-cell" x="150" y="154" width="150" height="86" rx="4"/><text class="dg-num" x="164" y="186" text-anchor="start">53</text><text class="dg-numlab" x="164" y="206" text-anchor="start">False positive</text><text class="dg-numlab" x="164" y="222" text-anchor="start">flagged, but they stayed</text><rect class="dg-cell" x="310" y="154" width="150" height="86" rx="4"/><text class="dg-num" x="324" y="186" text-anchor="start">839</text><text class="dg-numlab" x="324" y="206" text-anchor="start">True negative</text><text class="dg-numlab" x="324" y="222" text-anchor="start">not flagged, they stayed</text></svg><figcaption>1,000 customers, 108 of whom actually churned, at the default threshold of 0.5. Every classification metric is a different fraction built from these same four numbers.</figcaption></figure>

These numbers come from a churn model I simulated for these pages — 1,000
customers, 108 of whom actually left. Every figure on the next two
pages is derived from this same table, so they're all describing one
model rather than four different ones.

## Reading it

Say the four out loud in plain language once and the jargon stops being
slippery:

| Cell | Means | In this run |
|---|---|---|
| True positive | We flagged them, they churned | 75 |
| False positive | We flagged them, they stayed | 53 |
| False negative | We missed them, they churned | 33 |
| True negative | We left them alone, they stayed | 839 |

"Positive" just means the thing you're looking for — here, churn. "True"
and "false" describe whether the model was right. So a false negative is
the model saying *no* and being wrong about it.

## Why look at the table before the metrics

Because the two kinds of mistake have different price tags, and a single
score hides which one you're making.

In this run the model produced 53 false positives and 33 false negatives.
Those are not interchangeable:

- Each **false positive** costs one unnecessary retention call.
- Each **false negative** costs a customer who walked out while you were
  looking elsewhere.

If a retention call costs £5 and a lost customer costs £400, those 53
false positives cost about £265 and those 33 false negatives cost
about £13,200. Same model, and the errors you'd try to fix first are
obvious — but only once you've seen the table.

## Getting it

```python
from sklearn.metrics import confusion_matrix, classification_report

confusion_matrix(y_test, y_pred)     # [[839, 53], [33, 75]]
print(classification_report(y_test, y_pred))
```

Watch the layout. Scikit-learn orders it `[[839, 53], [33, 75]]` —
negatives first — while most textbooks and every diagram I'd seen put
true positives in the top-left. I read my own matrix backwards for a
while because of this.

## Where I got stuck

**Thinking of it as an output rather than a starting point.** I used to
glance at the matrix and move on to the metrics. It's the other way
round: the metrics are summaries of this table, and the table is where
you see which mistake you're actually making.

**Forgetting the column totals are fixed.** 108 customers churned in
this test set, full stop. Every threshold I try just moves them between
the "caught" and "missed" cells — it can't create more churners. Once
that clicked, the trade-off on the next two pages stopped feeling
arbitrary.
