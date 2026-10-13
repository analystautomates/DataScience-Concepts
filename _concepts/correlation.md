---
title: "Correlation"
section: statistics
order: 2
status: written
blurb: "How two variables move together."
---

Correlation puts a single number on whether two columns move together.
It runs from **-1 to +1**:

- **+1** — perfectly in step, up together
- **0** — no straight-line relationship at all
- **-1** — perfectly opposed, one up as the other goes down

The number people mean by default is Pearson's *r*.

## What different values look like

Numbers alone are hard to calibrate against, so this is the same pair of
columns under four different relationships:

<figure><svg viewBox="0 0 480 310" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Four scatter plots showing strong positive, weak positive, no, and negative correlation with their r values"><path class="dg-axis" d="M34 14 L34 118 L194 118" fill="none"/><circle class="dg-point" cx="77.1" cy="92.1" r="3.2"/><circle class="dg-point" cx="95.7" cy="80.4" r="3.2"/><circle class="dg-point" cx="131.7" cy="67.2" r="3.2"/><circle class="dg-point" cx="45.5" cy="106.4" r="3.2"/><circle class="dg-point" cx="80.1" cy="94.9" r="3.2"/><circle class="dg-point" cx="183.8" cy="30.8" r="3.2"/><circle class="dg-point" cx="161.4" cy="43.8" r="3.2"/><circle class="dg-point" cx="133.6" cy="64.8" r="3.2"/><circle class="dg-point" cx="133.0" cy="54.7" r="3.2"/><circle class="dg-point" cx="117.3" cy="65.8" r="3.2"/><circle class="dg-point" cx="138.1" cy="63.4" r="3.2"/><circle class="dg-point" cx="150.4" cy="48.6" r="3.2"/><circle class="dg-point" cx="86.0" cy="94.4" r="3.2"/><circle class="dg-point" cx="165.5" cy="41.5" r="3.2"/><circle class="dg-point" cx="144.8" cy="47.7" r="3.2"/><circle class="dg-point" cx="144.1" cy="47.4" r="3.2"/><circle class="dg-point" cx="99.2" cy="75.5" r="3.2"/><circle class="dg-point" cx="106.2" cy="69.4" r="3.2"/><circle class="dg-point" cx="167.3" cy="45.9" r="3.2"/><circle class="dg-point" cx="62.7" cy="105.3" r="3.2"/><circle class="dg-point" cx="179.5" cy="33.8" r="3.2"/><circle class="dg-point" cx="131.8" cy="63.7" r="3.2"/><text class="dg-strong" x="34" y="136" text-anchor="start">r = +0.98</text><path class="dg-axis" d="M274 14 L274 118 L434 118" fill="none"/><circle class="dg-point" cx="355.0" cy="85.9" r="3.2"/><circle class="dg-point" cx="333.0" cy="83.7" r="3.2"/><circle class="dg-point" cx="365.9" cy="47.2" r="3.2"/><circle class="dg-point" cx="379.6" cy="38.9" r="3.2"/><circle class="dg-point" cx="404.2" cy="22.9" r="3.2"/><circle class="dg-point" cx="378.1" cy="89.0" r="3.2"/><circle class="dg-point" cx="404.8" cy="24.3" r="3.2"/><circle class="dg-point" cx="411.0" cy="46.8" r="3.2"/><circle class="dg-point" cx="384.1" cy="83.0" r="3.2"/><circle class="dg-point" cx="400.7" cy="51.5" r="3.2"/><circle class="dg-point" cx="323.7" cy="113.8" r="3.2"/><circle class="dg-point" cx="403.8" cy="23.1" r="3.2"/><circle class="dg-point" cx="296.1" cy="87.9" r="3.2"/><circle class="dg-point" cx="341.4" cy="107.7" r="3.2"/><circle class="dg-point" cx="325.0" cy="75.8" r="3.2"/><circle class="dg-point" cx="406.5" cy="82.8" r="3.2"/><circle class="dg-point" cx="370.1" cy="100.5" r="3.2"/><circle class="dg-point" cx="384.8" cy="74.9" r="3.2"/><circle class="dg-point" cx="407.6" cy="21.9" r="3.2"/><circle class="dg-point" cx="354.8" cy="46.5" r="3.2"/><circle class="dg-point" cx="327.2" cy="113.8" r="3.2"/><circle class="dg-point" cx="368.0" cy="102.4" r="3.2"/><text class="dg-strong" x="274" y="136" text-anchor="start">r = +0.66</text><path class="dg-axis" d="M34 174 L34 278 L194 278" fill="none"/><circle class="dg-point" cx="71.4" cy="234.4" r="3.2"/><circle class="dg-point" cx="129.6" cy="257.5" r="3.2"/><circle class="dg-point" cx="49.6" cy="192.3" r="3.2"/><circle class="dg-point" cx="87.8" cy="184.0" r="3.2"/><circle class="dg-point" cx="169.8" cy="237.2" r="3.2"/><circle class="dg-point" cx="108.4" cy="224.2" r="3.2"/><circle class="dg-point" cx="134.3" cy="217.2" r="3.2"/><circle class="dg-point" cx="122.3" cy="215.0" r="3.2"/><circle class="dg-point" cx="176.0" cy="225.4" r="3.2"/><circle class="dg-point" cx="104.3" cy="205.8" r="3.2"/><circle class="dg-point" cx="77.1" cy="244.2" r="3.2"/><circle class="dg-point" cx="181.3" cy="224.1" r="3.2"/><circle class="dg-point" cx="120.8" cy="270.7" r="3.2"/><circle class="dg-point" cx="102.1" cy="218.7" r="3.2"/><circle class="dg-point" cx="46.4" cy="215.4" r="3.2"/><circle class="dg-point" cx="132.6" cy="266.3" r="3.2"/><circle class="dg-point" cx="131.9" cy="229.1" r="3.2"/><circle class="dg-point" cx="139.2" cy="239.5" r="3.2"/><circle class="dg-point" cx="143.1" cy="204.2" r="3.2"/><circle class="dg-point" cx="46.7" cy="266.2" r="3.2"/><circle class="dg-point" cx="138.8" cy="183.6" r="3.2"/><circle class="dg-point" cx="79.0" cy="230.0" r="3.2"/><text class="dg-strong" x="34" y="296" text-anchor="start">r = -0.04</text><path class="dg-axis" d="M274 174 L274 278 L434 278" fill="none"/><circle class="dg-point" cx="367.0" cy="231.6" r="3.2"/><circle class="dg-point" cx="334.8" cy="214.0" r="3.2"/><circle class="dg-point" cx="335.6" cy="207.9" r="3.2"/><circle class="dg-point" cx="325.9" cy="207.6" r="3.2"/><circle class="dg-point" cx="392.3" cy="252.3" r="3.2"/><circle class="dg-point" cx="363.8" cy="220.3" r="3.2"/><circle class="dg-point" cx="327.3" cy="211.8" r="3.2"/><circle class="dg-point" cx="396.8" cy="249.9" r="3.2"/><circle class="dg-point" cx="310.0" cy="197.4" r="3.2"/><circle class="dg-point" cx="381.9" cy="244.8" r="3.2"/><circle class="dg-point" cx="328.9" cy="210.2" r="3.2"/><circle class="dg-point" cx="401.0" cy="247.6" r="3.2"/><circle class="dg-point" cx="404.1" cy="255.5" r="3.2"/><circle class="dg-point" cx="331.0" cy="204.1" r="3.2"/><circle class="dg-point" cx="408.2" cy="251.3" r="3.2"/><circle class="dg-point" cx="315.3" cy="207.6" r="3.2"/><circle class="dg-point" cx="358.2" cy="229.7" r="3.2"/><circle class="dg-point" cx="397.2" cy="236.4" r="3.2"/><circle class="dg-point" cx="309.4" cy="200.7" r="3.2"/><circle class="dg-point" cx="397.3" cy="240.9" r="3.2"/><circle class="dg-point" cx="397.1" cy="247.6" r="3.2"/><circle class="dg-point" cx="301.9" cy="196.2" r="3.2"/><text class="dg-strong" x="274" y="296" text-anchor="start">r = -0.97</text></svg><figcaption>Same two columns, four different stories. Correlation only measures how tightly the points hug a straight line, and the sign only tells you which way that line tilts.</figcaption></figure>

Rough reading for everyday work: above 0.7 is strong, 0.3 to 0.7 is
worth investigating, below 0.3 rarely survives contact with new data.
These are conventions, not thresholds — and they shift by field.

## Getting it

```python
df[['spend', 'signups']].corr()   # the pair
df.corr(numeric_only=True)        # every pair at once
```

That second one is a good first move on any new dataset. It's also the
quickest way to notice that two of your input columns are nearly
identical, which quietly wrecks regression coefficients.

## The three things r won't tell you

**It only sees straight lines.** This is the one that genuinely surprised
me:

<figure><svg viewBox="0 0 480 245" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Scatter plot forming a clear inverted-U curve with a correlation coefficient close to zero"><path class="dg-axis" d="M55 20 L55 190 L435 190" fill="none"/><circle class="dg-point" cx="74.0" cy="165.4" r="4"/><circle class="dg-point" cx="91.1" cy="139.8" r="4"/><circle class="dg-point" cx="108.2" cy="117.7" r="4"/><circle class="dg-point" cx="125.3" cy="96.7" r="4"/><circle class="dg-point" cx="142.4" cy="83.1" r="4"/><circle class="dg-point" cx="159.5" cy="66.7" r="4"/><circle class="dg-point" cx="176.6" cy="67.2" r="4"/><circle class="dg-point" cx="193.7" cy="52.7" r="4"/><circle class="dg-point" cx="210.8" cy="40.0" r="4"/><circle class="dg-point" cx="227.9" cy="40.0" r="4"/><circle class="dg-point" cx="245.0" cy="35.5" r="4"/><circle class="dg-point" cx="262.1" cy="47.2" r="4"/><circle class="dg-point" cx="279.2" cy="46.3" r="4"/><circle class="dg-point" cx="296.3" cy="55.5" r="4"/><circle class="dg-point" cx="313.4" cy="60.4" r="4"/><circle class="dg-point" cx="330.5" cy="71.4" r="4"/><circle class="dg-point" cx="347.6" cy="92.7" r="4"/><circle class="dg-point" cx="364.7" cy="106.3" r="4"/><circle class="dg-point" cx="381.8" cy="124.5" r="4"/><circle class="dg-point" cx="398.9" cy="137.5" r="4"/><circle class="dg-point" cx="416.0" cy="163.6" r="4"/><text class="dg-strong" x="60" y="215" text-anchor="start">r = -0.03</text><text class="dg-label" x="60" y="234" text-anchor="start">and yet the relationship is obvious</text></svg><figcaption>A near-perfect relationship that correlation scores at roughly zero. This is why plotting the data first is not optional.</figcaption></figure>

A relationship you could describe in one sentence, and correlation scores
it at almost nothing. Plot first. Always.

**One outlier can invent it, or hide it.** With 30 rows, a single extreme
point can drag *r* from 0.1 to 0.6. If a correlation appears or vanishes
when you remove one row, you don't have a finding.

**Correlation isn't causation.** The familiar one, but the useful version
is more specific. When A and B correlate, there are four live
possibilities: A causes B, B causes A, something else causes both, or
it's coincidence. Nothing in the number distinguishes between them. Ice
cream sales and drowning deaths correlate strongly — the cause of both is
summer.

## Pearson vs Spearman

Pearson measures straight-line relationships. **Spearman** correlates the
*ranks* instead, so it catches any relationship that moves consistently
in one direction, even a curved one, and it barely flinches at outliers.

```python
df.corr(method='spearman')
```

Rule of thumb I use now: if the two disagree a lot, the relationship
isn't linear — go and look at the scatter plot.

## Where I got stuck

**Hearing 0.7 as "most of it".** Square it. An *r* of 0.7 means roughly
49% of the variation is shared, about half, not most. An *r* of 0.3,
which still looks respectable in a correlation matrix, is 9%.

**Reporting correlations from a matrix I hadn't plotted.** Twenty columns
gives you 190 pairs, and a few will correlate by sheer chance. Hunting a
big matrix for high numbers and reporting the winners is a reliable way
to present noise as insight — a mistake that's only obvious once it's
pointed out.
