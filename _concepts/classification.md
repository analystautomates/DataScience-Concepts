---
title: "Classification"
section: ml-fundamentals
order: 2
status: written
blurb: "Predicting a category."
---

Classification is for when the answer is a **category**, not a number.
Will this customer churn? Is this transaction fraud? Which of five plans
will they pick?

Same machinery as [regression]({{ '/learn/regression/' | relative_url }}),
different output, and — importantly — completely different metrics.

## The idea

The model learns a boundary through your data that separates one class
from another. New point lands on one side, it gets that label.

<figure><svg viewBox="0 0 480 265" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Scatter plot of two customer groups separated by a dashed decision boundary, with one misclassified point circled"><path class="dg-axis" d="M55 25 L55 225 L445 225" fill="none"/><line class="dg-dash" x1="77.8" y1="213.3" x2="422.3" y2="36.7"/><circle class="dg-open" cx="336.8" cy="143.7" r="4.5"/><circle class="dg-open" cx="356.3" cy="162.3" r="4.5"/><circle class="dg-open" cx="284.1" cy="155.7" r="4.5"/><circle class="dg-open" cx="331.2" cy="150.0" r="4.5"/><circle class="dg-open" cx="336.8" cy="142.3" r="4.5"/><circle class="dg-open" cx="326.0" cy="160.8" r="4.5"/><circle class="dg-open" cx="355.0" cy="187.7" r="4.5"/><circle class="dg-open" cx="311.8" cy="175.5" r="4.5"/><circle class="dg-open" cx="408.6" cy="167.0" r="4.5"/><circle class="dg-open" cx="354.7" cy="152.2" r="4.5"/><circle class="dg-open" cx="316.6" cy="197.3" r="4.5"/><circle class="dg-open" cx="367.3" cy="173.5" r="4.5"/><circle class="dg-point" cx="224.3" cy="54.8" r="4.5"/><circle class="dg-point" cx="174.6" cy="101.0" r="4.5"/><circle class="dg-point" cx="127.5" cy="84.3" r="4.5"/><circle class="dg-point" cx="130.4" cy="115.0" r="4.5"/><circle class="dg-point" cx="180.1" cy="82.2" r="4.5"/><circle class="dg-point" cx="194.1" cy="104.0" r="4.5"/><circle class="dg-point" cx="172.3" cy="86.3" r="4.5"/><circle class="dg-point" cx="110.9" cy="73.8" r="4.5"/><circle class="dg-point" cx="180.1" cy="88.0" r="4.5"/><circle class="dg-point" cx="222.0" cy="80.8" r="4.5"/><circle class="dg-point" cx="209.1" cy="92.7" r="4.5"/><circle class="dg-point" cx="302.0" cy="125.0" r="4.5"/><circle cx="302.0" cy="125.0" r="10" class="dg-resid" fill="none"/><text class="dg-label" x="317" y="129" text-anchor="start">predicted wrong</text><text class="dg-label" x="55" y="250" text-anchor="start">Months as a customer</text><text class="dg-label" text-anchor="middle" transform="rotate(-90 18 125)" x="18" y="125">Support tickets</text><text class="dg-cat" x="84" y="38" text-anchor="start">churned</text><text class="dg-label" x="360" y="210" text-anchor="start">stayed</text></svg><figcaption>Filled dots churned, hollow dots stayed. The dashed line is the boundary the model learned. One customer sits on the wrong side of it — that is normal, and it is what the evaluation metrics measure.</figcaption></figure>

Notice the circled dot. The boundary doesn't separate the two groups
perfectly and it never will, because real customers don't sort themselves
cleanly. The entire discipline of
[model evaluation]({{ '/learn/accuracy/' | relative_url }}) exists to put
a number on how much that matters.

## It predicts probabilities, not labels

This took me longer to absorb than it should have. The model doesn't
decide "churn". It outputs something like 0.73 — its confidence. The
label only appears when you compare that to a **threshold**.

<figure><svg viewBox="0 0 480 100" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="A horizontal scale from zero to one with customer probabilities marked and a threshold line at 0.5"><line class="dg-axis" x1="45.0" y1="60" x2="435.0" y2="60"/><line class="dg-dash" x1="240.0" y1="20" x2="240.0" y2="78"/><circle class="dg-open" cx="60.6" cy="60" r="5"/><circle class="dg-open" cx="87.9" cy="60" r="5"/><circle class="dg-open" cx="119.1" cy="60" r="5"/><circle class="dg-open" cx="169.8" cy="60" r="5"/><circle class="dg-open" cx="204.9" cy="60" r="5"/><circle class="dg-open" cx="232.2" cy="60" r="5"/><circle class="dg-point" cx="259.5" cy="60" r="5"/><circle class="dg-point" cx="290.7" cy="60" r="5"/><circle class="dg-point" cx="349.2" cy="60" r="5"/><circle class="dg-point" cx="380.4" cy="60" r="5"/><circle class="dg-point" cx="411.6" cy="60" r="5"/><text class="dg-label" x="45" y="92" text-anchor="start">0.0 — definitely stays</text><text class="dg-label" x="435" y="92" text-anchor="end">certainly churns — 1.0</text><text class="dg-cat" x="240" y="14" text-anchor="middle">threshold 0.5</text></svg><figcaption>The model actually outputs a probability for each customer. The threshold is a separate decision you make, and moving it changes who gets flagged without retraining anything.</figcaption></figure>

The default threshold is 0.5, and there is nothing special about 0.5. It
is a business decision wearing a maths costume.

- Chasing a customer who wasn't going to leave costs you one phone call.
- Missing one who was costs you the whole account.

Given that, 0.5 is probably too high. Lower it to 0.3 and you catch more
leavers while bothering more people who were staying anyway. Moving the
threshold doesn't require retraining — it's a dial you turn afterwards,
and it's the fastest useful lever you have.

## Doing it

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression()
model.fit(X_train, y_train)

model.predict(X_test)                    # labels, using 0.5
model.predict_proba(X_test)[:, 1]        # the probabilities themselves
```

Reach for `predict_proba` more often than `predict`. Once you have the
probability you can set your own threshold, rank customers by risk, and
decide how far down the list your team has capacity to go.

## Where I got stuck

**Trusting accuracy.** If 3% of customers churn, a model that predicts
"nobody churns" is 97% accurate and completely worthless. I built one of
these. It looked great until I checked what it had actually predicted.

That single trap is why
[precision]({{ '/learn/precision/' | relative_url }}),
[recall]({{ '/learn/recall/' | relative_url }}) and the
[confusion matrix]({{ '/learn/confusion-matrix/' | relative_url }})
exist, and why I'm writing those up next.

**Expecting a clean boundary.** I kept tuning, assuming a good enough
model would separate the classes properly. Some overlap is irreducible,
two identical looking customers genuinely do different things. The goal
is a boundary that's useful, not one that's perfect.
