---
title: "Regression"
section: ml-fundamentals
order: 1
status: written
blurb: "Predicting a number."
---

Regression is what you use when the answer you want is a **number**.
How much will this customer spend? How many tickets will we get next
week? What should this house sell for?

If the answer is a label rather than a number, churn or not, spam or
not.... that's [classification]({{ '/learn/classification/' | relative_url }})
instead. That one distinction decides almost everything else: which model
you reach for, and which metrics mean anything.

## The idea

You have some inputs and a number you want to predict. Regression finds
the relationship between them and writes it down as an equation you can
reuse on data you haven't seen.

The simplest version draws a straight line through your data.

<figure><svg viewBox="0 0 480 265" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Scatter plot of ad spend against signups with a fitted straight line and vertical residual lines from each point to the line"><path class="dg-axis" d="M55 25 L55 225 L445 225" fill="none"/><line class="dg-line" x1="71.2" y1="179.5" x2="428.8" y2="67.9"/><line class="dg-resid" x1="120.0" y1="164.7" x2="120.0" y2="164.3"/><line class="dg-resid" x1="152.5" y1="161.3" x2="152.5" y2="154.1"/><line class="dg-resid" x1="185.0" y1="131.0" x2="185.0" y2="144.0"/><line class="dg-resid" x1="217.5" y1="143.7" x2="217.5" y2="133.9"/><line class="dg-resid" x1="250.0" y1="115.0" x2="250.0" y2="123.7"/><line class="dg-resid" x1="282.5" y1="111.3" x2="282.5" y2="113.6"/><line class="dg-resid" x1="315.0" y1="113.3" x2="315.0" y2="103.4"/><line class="dg-resid" x1="347.5" y1="85.0" x2="347.5" y2="93.3"/><line class="dg-resid" x1="380.0" y1="93.7" x2="380.0" y2="83.1"/><line class="dg-resid" x1="412.5" y1="67.3" x2="412.5" y2="73.0"/><circle class="dg-point" cx="120.0" cy="164.7" r="4.5"/><circle class="dg-point" cx="152.5" cy="161.3" r="4.5"/><circle class="dg-point" cx="185.0" cy="131.0" r="4.5"/><circle class="dg-point" cx="217.5" cy="143.7" r="4.5"/><circle class="dg-point" cx="250.0" cy="115.0" r="4.5"/><circle class="dg-point" cx="282.5" cy="111.3" r="4.5"/><circle class="dg-point" cx="315.0" cy="113.3" r="4.5"/><circle class="dg-point" cx="347.5" cy="85.0" r="4.5"/><circle class="dg-point" cx="380.0" cy="93.7" r="4.5"/><circle class="dg-point" cx="412.5" cy="67.3" r="4.5"/><text class="dg-label" x="55" y="250" text-anchor="start">Ad spend (£k)</text><text class="dg-label" text-anchor="middle" transform="rotate(-90 18 125)" x="18" y="125">Signups</text><text class="dg-cat" x="84" y="48" text-anchor="start">the fitted line</text></svg><figcaption>Each dot is one week. The line is the model's prediction; the short vertical ticks are how wrong it was. Fitting means choosing the one line that makes those ticks as small as possible overall.</figcaption></figure>

The line here is `signups = 12.1 + 3.0 x spend`. The useful part is the
3.0: every extra £1k of spend came with about 3 more signups. That number
is the model.

## What "fitting" actually means

Any line you draw will miss most of the points. The gap between a real
value and the line is the **residual**, and the fitting process picks the
line that makes those residuals smallest overall.

Specifically, it minimises the *sum of the squared* residuals. Squaring
does two things: it stops positive and negative misses cancelling out,
and it punishes one big miss far more than several small ones. That's
also why outliers drag the line around so hard — a residual of 10 counts
a hundred times as much as a residual of 1.

## Doing it

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)

model.coef_        # the 3.1 — one per input column
model.intercept_   # the 13.4
model.predict(X_new)
```

Three lines. The hard part was never the fitting.

## How you know it's any good

Two numbers worth looking at first:

| Metric | Reads as |
|---|---|
| MAE | On average, predictions are off by this much — in real units |
| R² | The share of the variation the model accounts for, 0 to 1 |

MAE is the one to quote to a stakeholder, because "off by about 40
signups" means something to everybody. R² is useful for comparing two
models on the same data and misleading for almost anything else.

Check both on data the model has never seen. Scoring your model on the
rows you trained it on tells you nothing — see
[train/test split]({{ '/learn/train-test-split/' | relative_url }}).

## Where I got stuck

**Thinking "linear" meant straight lines only.** It doesn't. It means
linear in the *coefficients*. You can feed in `spend²` or `log(spend)` as
a column and still use linear regression — the model stays linear, the
curve doesn't. That's [feature engineering]({{ '/learn/feature-engineering/' | relative_url }}),
and it's most of the job.

**Reading coefficients as causes.** A coefficient of 3.0 says that in
this data, higher spend came with more signups. It does not promise that
spending another £1k will produce 3 more. Observational data can't tell
you that, no matter how good the fit looks.
