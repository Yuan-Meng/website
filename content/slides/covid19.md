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

# What do we know so far?

---

## Fatality rate by age

<figure>
  <img src="/img/age.png" align=top height="320" hspace="-10" />
</figure>

- Similarly low for patients under 40
- Increases sharply from 60+ to 80+

---

## Fatality rate by pre-existing conditions

<figure>
  <img src="/img/preconditions.png" align=top width="400" hspace="-10" />
</figure>

- Patients with certain pre-existing conditions are far more likely to die than healthy patients 

---

## Fatality rate by sex

<figure>
  <img src="/img/sex.png" align=top width="500" hspace="-10" />
</figure>

- Male patients are about 1.6 times more likely to die compared to female patients

---

## You may still wonder...

<ul>
{{% fragment %}}<li>Yes, I know COVID-19 hits older people harder, but <b>how much harder</b>?</li>{{% /fragment %}}
{{% fragment %}}<li>Is a <b>healthy 80-year-old</b> or a <b>20-year-old with diabetes</b> at higher risk?</li>{{% /fragment %}}
{{% fragment %}}<li>What about <b>my community</b>? Do risk factors and their relative importance differ by region?</li>{{% /fragment %}}
</ul>

{{% fragment %}}...{{% /fragment %}}

---

## My goals

<ul>
{{% fragment %}}<li>Predict <b>gradient</b> risk, not just "higher" or "lower"</li>{{% /fragment %}}
{{% fragment %}}<li>Combine <b>multiple factors</b> to evaluate risk</li>{{% /fragment %}}
{{% fragment %}}<li>Make predictions <b>specific to each community</b></li>{{% /fragment %}}
{{% fragment %}}<li>Create a <b>web or mobile app</b> for users to look up</li>{{% /fragment %}}
</ul>

---

## Current work

<ul>
{{% fragment %}}<li>Obtained <a href="https://github.com/beoutbreakprepared/nCoV2019/tree/master/latest_data">data</a> of 266,874 COVID-19 patients</li>{{% /fragment %}} 
{{% fragment %}}<li>Among them, 1,005 had outcome information (e.g., died, recovered, in treatment)</li>{{% /fragment %}}
</ul>

<figure>
  <img src="/img/snapshot.png" align=top width="700" hspace="-10" />
</figure>

---

## Current work

<ul>
{{% fragment %}}<li>Trained an SVM classifier on 12 features (2 demographic, 8 clinical, 2 medical resources)</li>{{% /fragment %}} 
{{% fragment %}}<li><b>Great performance</b>: F1 score = .91, AUC = .95 in test; F1 score = .92, AUC = .91 in full dataset</li>{{% /fragment %}}
</ul>

<figure>
  <img src="/img/eval.png" align=top width="620" />
</figure>

---

## Current work

Deployed the trained classifier as a Heroku web app → take user input to make new predictions

<iframe frameborder="0" width="100%" height="500pt" src="https://covid19-risk.herokuapp.com/"></iframe>

---

## Extending this work at TDI

<ul>
{{% fragment %}}<li><b>Retrain and re-deploy models</b> online as more patient data becomes available</li>{{% /fragment %}}
{{% fragment %}}<li>Incorporate <b>local information</b> (e.g., medical shortages, stay-at-home policies, population density) to make finer predictions </li>{{% /fragment %}}
{{% fragment %}}<li>Create a more versatile app that allows users, for instance, to <b>select models and features</b> to use</li>{{% /fragment %}}
{{% fragment %}}<li>Statistically <b>correct for biases</b> in data reporting</li>{{% /fragment %}}
</ul>

{{% fragment %}}...{{% fragment %}}


---

# Questions?

[Web App](https://covid19-risk.herokuapp.com/)

[GitHub](https://github.com/Yuan-Meng/COVID-19)

<a href="mailto:yuan_meng@berkeley.edu">Email</a>
