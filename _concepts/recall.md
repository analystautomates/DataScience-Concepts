---
title: "Recall"
section: model-evaluation
order: 3
status: written
blurb: "How many real cases got caught."
---

Recall answers the mirror-image question to
[precision]({{ '/learn/precision/' | relative_url }}): **of all the cases
that were really out there, how many did we catch?**

```
recall = true positives / (true positives + false negatives)
```

Same [confusion matrix]({{ '/learn/confusion-matrix/' | relative_url }}),
different slice. Precision reads a column; recall reads a row.

<figure><svg viewBox="0 0 480 265" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="The same confusion matrix with the two 'actually churned' cells highlighted"><text class="dg-strong" x="225" y="30" text-anchor="middle">Model said churn</text><text class="dg-strong" x="385" y="30" text-anchor="middle">Model said stay</text><text class="dg-strong" x="140" y="106" text-anchor="end">Actually churned</text><text class="dg-strong" x="140" y="202" text-anchor="end">Actually stayed</text><rect class="dg-hi" x="150" y="58" width="150" height="86" rx="4"/><rect class="dg-cell" x="150" y="58" width="150" height="86" rx="4"/><text class="dg-num" x="164" y="90" text-anchor="start">75</text><text class="dg-numlab" x="164" y="110" text-anchor="start">True positive</text><text class="dg-numlab" x="164" y="126" text-anchor="start">flagged, and they left</text><rect class="dg-hi" x="310" y="58" width="150" height="86" rx="4"/><rect class="dg-cell" x="310" y="58" width="150" height="86" rx="4"/><text class="dg-num" x="324" y="90" text-anchor="start">33</text><text class="dg-numlab" x="324" y="110" text-anchor="start">False negative</text><text class="dg-numlab" x="324" y="126" text-anchor="start">missed, and they left</text><rect class="dg-cell" x="150" y="154" width="150" height="86" rx="4"/><text class="dg-num" x="164" y="186" text-anchor="start">53</text><text class="dg-numlab" x="164" y="206" text-anchor="start">False positive</text><text class="dg-numlab" x="164" y="222" text-anchor="start">flagged, but they stayed</text><rect class="dg-cell" x="310" y="154" width="150" height="86" rx="4"/><text class="dg-num" x="324" y="186" text-anchor="start">839</text><text class="dg-numlab" x="324" y="206" text-anchor="start">True negative</text><text class="dg-numlab" x="324" y="222" text-anchor="start">not flagged, they stayed</text></svg><figcaption>Recall reads the top row: of everyone who actually churned, what share did we catch. The false positives are invisible to it.</figcaption></figure>

In this run: 108 customers actually churned, the model caught 75 of
them. Recall is **69%**. The remaining 33 left without ever being
flagged.

## What it's for

Recall is what matters when **missing a case is the expensive mistake**.

- Screening for disease — a missed diagnosis is far worse than a second
  test.
- Fraud detection — a missed fraudulent transaction is a direct loss.
- Churn — a customer who leaves unnoticed is gone; a false alarm costs a
  phone call.

The pattern: whenever the damage from a miss outweighs the cost of a
false alarm, optimise recall.

## The trade-off, drawn

You cannot maximise both. Tightening the threshold to raise precision
means flagging fewer people, which means catching fewer churners.

<figure><svg viewBox="0 0 480 240" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Line chart showing precision rising and recall falling as the decision threshold increases"><path class="dg-axis" d="M58 25 L58 205 L438 205" fill="none"/><line class="dg-grid" x1="58.0" y1="160.0" x2="438.0" y2="160.0"/><line class="dg-grid" x1="58.0" y1="115.0" x2="438.0" y2="115.0"/><line class="dg-grid" x1="58.0" y1="70.0" x2="438.0" y2="70.0"/><polyline class="dg-line" points="77.0,182.2 80.8,181.8 84.6,181.5 88.4,181.3 92.2,180.9 96.0,180.5 99.8,180.4 103.6,179.8 107.4,179.1 111.2,178.2 115.0,177.4 118.8,176.5 122.6,175.3 126.4,174.0 130.2,173.2 134.0,172.5 137.8,171.6 141.6,170.8 145.4,170.1 149.2,168.2 153.0,167.0 156.8,164.6 160.6,163.9 164.4,162.6 168.2,160.3 172.0,158.0 175.8,156.2 179.6,154.7 183.4,153.3 187.2,149.9 191.0,147.7 194.8,145.4 198.6,143.5 202.4,139.9 206.2,135.6 210.0,133.5 213.8,130.6 217.6,129.1 221.4,125.5 225.2,124.0 229.0,119.6 232.8,112.2 236.6,112.1 240.4,108.8 244.2,104.4 248.0,99.5 251.8,92.1 255.6,81.0 259.4,78.5 263.2,72.4 267.0,67.5 270.8,56.5 274.6,53.1 278.4,53.3 282.2,51.5 286.0,49.5 289.8,49.0 293.6,47.1 297.4,42.3 301.2,42.3 305.0,42.6 308.8,43.4 312.6,44.1 316.4,42.1 320.2,38.5 324.0,38.8 327.8,39.6 331.6,40.4 335.4,40.9 339.2,37.0 343.0,37.0 346.8,37.9 350.6,37.9 354.4,37.9 358.2,38.3 362.0,32.5 365.8,32.8 369.6,33.6 373.4,34.5 377.2,25.0 381.0,25.0 384.8,25.0 388.6,25.0 392.4,25.0 396.2,25.0 400.0,25.0 403.8,25.0 407.6,25.0 411.4,25.0 415.2,25.0 419.0,25.0"/><polyline class="dg-line2" points="77.0,26.7 80.8,26.7 84.6,26.7 88.4,26.7 92.2,26.7 96.0,26.7 99.8,28.3 103.6,28.3 107.4,28.3 111.2,28.3 115.0,28.3 118.8,28.3 122.6,28.3 126.4,28.3 130.2,28.3 134.0,28.3 137.8,28.3 141.6,31.7 145.4,33.3 149.2,33.3 153.0,35.0 156.8,35.0 160.6,36.7 164.4,38.3 168.2,38.3 172.0,38.3 175.8,38.3 179.6,41.7 183.4,41.7 187.2,41.7 191.0,41.7 194.8,41.7 198.6,43.3 202.4,43.3 206.2,45.0 210.0,46.7 213.8,50.0 217.6,56.7 221.4,60.0 225.2,63.3 229.0,65.0 232.8,68.3 236.6,71.7 240.4,76.7 244.2,78.3 248.0,80.0 251.8,81.7 255.6,83.3 259.4,86.7 263.2,88.3 267.0,91.7 270.8,95.0 274.6,96.7 278.4,106.7 282.2,108.3 286.0,110.0 289.8,118.3 293.6,121.7 297.4,126.7 301.2,126.7 305.0,128.3 308.8,131.7 312.6,135.0 316.4,141.7 320.2,143.3 324.0,145.0 327.8,148.3 331.6,151.7 335.4,153.3 339.2,158.3 343.0,158.3 346.8,161.7 350.6,161.7 354.4,161.7 358.2,163.3 362.0,166.7 365.8,168.3 369.6,171.7 373.4,175.0 377.2,178.3 381.0,183.3 384.8,185.0 388.6,188.3 392.4,188.3 396.2,191.7 400.0,195.0 403.8,195.0 407.6,196.7 411.4,196.7 415.2,196.7 419.0,196.7"/><line class="dg-dash" x1="248.0" y1="205.0" x2="248.0" y2="25.0"/><text class="dg-cat" x="324" y="72" text-anchor="start">precision</text><text class="dg-label" x="294" y="174" text-anchor="start">recall</text><text class="dg-label" x="248" y="18" text-anchor="middle">default 0.5</text><text class="dg-label" x="58" y="228" text-anchor="start">Threshold</text><text class="dg-label" text-anchor="middle" transform="rotate(-90 20 115)" x="20" y="115">Score</text><text class="dg-label" x="52" y="209" text-anchor="end">0</text><text class="dg-label" x="52" y="119" text-anchor="end">0.5</text><text class="dg-label" x="52" y="29" text-anchor="end">1.0</text></svg><figcaption>Turning the threshold up buys precision and sells recall. There is no setting that maximises both, which is the entire reason you have to decide which error costs you more.</figcaption></figure>

Pick a point on that x-axis and you have chosen your error profile. The
default of 0.5 is a choice too — just one made by a library author who
knew nothing about your business.

Rough rule I use now: if a false alarm costs £5 and a miss costs £400,
you should be willing to accept a lot of false alarms. Push the threshold
down until the team's capacity to follow up runs out.

## Getting it

```python
from sklearn.metrics import recall_score

recall_score(y_test, y_pred)
```

If you want one number covering both sides, that's
[F1]({{ '/learn/f1/' | relative_url }}) — the harmonic mean of precision
and recall, which here works out at 64%.

## Where I got stuck

**Chasing high recall and declaring victory.** Flag every single customer
and recall is 100%. It is trivially achievable and worthless, in exactly
the way perfect precision is trivially achievable and worthless. The two
numbers only mean something side by side.

**Not realising accuracy hides all of this.** This is the trap I walked
into properly:

<figure><svg viewBox="0 0 480 190" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Bar chart comparing the accuracy of a do-nothing baseline against the real model"><path class="dg-axis" d="M70 30 L70 160 L430 160" fill="none"/><rect class="dg-bar-ghost" x="93" y="44" width="86" height="116" rx="3"/><text class="dg-num" x="136" y="34" text-anchor="middle">89.2%</text><text class="dg-label" x="136" y="180" text-anchor="middle">Always say 'stays'</text><rect class="dg-bar" x="249" y="41" width="86" height="119" rx="3"/><text class="dg-num" x="292" y="31" text-anchor="middle">91.4%</text><text class="dg-label" x="292" y="180" text-anchor="middle">The actual model</text><text class="dg-label" x="357" y="85" text-anchor="start">same ballpark,</text><text class="dg-strong" x="357" y="102" text-anchor="start">one is useless</text></svg><figcaption>A model that predicts 'nobody churns' never finds a single churner, and still scores 89.2%. That is the number accuracy reports when one class is rare.</figcaption></figure>

The do-nothing baseline catches zero churners and still posts a number
that would look fine in a status update. Our model's accuracy is only a
little higher, and yet it finds 69% of leavers. Accuracy couldn't
tell those two apart — the whole reason precision and recall exist.
