---
title: COVID-19 Risk Predictor
summary: 
authors: [Yuan Meng]
tags: []
categories: []
date: "2020-04-12"
slides:
  # Choose a theme from https://github.com/hakimel/reveal.js#theming
  theme: white
  # Choose a code highlighting style (if highlighting enabled in `params.toml`)
  #   Light style: github. Dark style: dracula (default).
  highlight_style: dracula
   
---

# COVID-19 Risk Predictor

Yuan Meng

[Code](https://github.com/Yuan-Meng/COVID-19) | [Web App](https://covid19-risk.herokuapp.com/)

---

# If I get COVID-19, will I survive or die? 

---

# What I've done so far

---

## Data
<ul>
{{% fragment %}}<li>Obtained <a href="https://github.com/beoutbreakprepared/nCoV2019/tree/master/latest_data">data</a> from the <a href="https://github.com/beoutbreakprepared/nCoV2019">University of Washington</a></li>{{% /fragment %}} 
{{% fragment %}}<li>266,874 COVID-19 patients → 1,005 with outcomes (e.g., died, recovered, in treatment)</li>{{% /fragment %}}
</ul>

<figure>
  <img src="/img/snapshot.png" align=top width="700" hspace="-10" />
</figure>

---

## Classifier

<ul>
{{% fragment %}}<li><b>Features</b>: Trained an SVM classifier on 12 features (demographic: 2, clinical: 8, medical resources: 8)</li>{{% /fragment %}} 
{{% fragment %}}<li><b>Performance</b>: F1 score = .91, AUC = .95 in test; F1 score = .92, AUC = .91 in full dataset</li>{{% /fragment %}}
</ul>

<figure>
  <img src="/img/eval.png" align=top width="620" />
</figure>

---

## Web App

Deployed the trained classifier as a Heroku web app → take user input to make new predictions

<iframe frameborder="0" width="100%" height="500pt" src="https://covid19-risk.herokuapp.com/"></iframe>

---

## Extending this work at TDI

<ul>
{{% fragment %}}<li><b>Retrain and re-deploy models</b> online as more patient data becomes available</li>{{% /fragment %}}
{{% fragment %}}<li>Incorporate <b>state- or county-level data</b> (e.g., medical shortages, stay-at-home policies, population density) to make finer predictions </li>{{% /fragment %}}
{{% fragment %}}<li>Create a more versatile app that allows users to <b>select models and features</b> to use</li>{{% /fragment %}}
</ul>

{{% fragment %}}...{{% fragment %}}

---

# Questions?

[Web App](https://covid19-risk.herokuapp.com/)

[GitHub](https://github.com/Yuan-Meng/COVID-19)

<a href="mailto:yuan_meng@berkeley.edu">Email</a>

---

## Contributions

- Older patients are hit harder, but how much harder? **→ Make predictions in a gradient manner** 
- Healthy 80-year-old vs. 20-year-old with chronic diseases? **→Combine multiple factors**
- **Convenience:** Users can look up their risk on their mobile phone or web browser w/o ML

