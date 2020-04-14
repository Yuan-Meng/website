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

{{< speaker_note >}}
- The project I'll be proposing today is a COVID-19 risk predictor. 
{{< /speaker_note >}}

---

# If I get COVID-19, will I survive or die? 

{{< speaker_note >}}
- The end product will be a web app that predicts users' mortality risk should they contract COVID-19.
- Knowing the answer helps hospitals better allocate resources and prompt people to rethink their reckless behaviors.
{{< /speaker_note >}}

---

# What I've done so far

{{< speaker_note >}}
- Here's what I've done so far.
{{< /speaker_note >}}

---

## Data

- Obtained <a href="https://github.com/beoutbreakprepared/nCoV2019/tree/master/latest_data">data</a> from <a href="https://github.com/beoutbreakprepared/nCoV2019">UW</a>: 266,874 COVID-19 patients, 1,005 with outcomes (died, ICU, etc.)
- US has most cases; half under 48; most survived

<figure><img src="/img/viz.png" align=top width="700" hspace="-10" /></figure>

{{< speaker_note >}}
- First, I obtained patient data from researchers at the University of Washington.
- Their dataset has nearly 300 thousand patients with outcomes for about 1,000.
- (As expected, the US now has most patients. About half of patients are under 48. Most survived.)
{{< /speaker_note >}}

---

## Classifier


- Trained an SVM classifier using **demographic** (2), **clinical** (8) and **medical resources** (2) features → F1 score = .91, AUC = .95 in testing
- **Most important**: doctors per 10k residents, age

<figure><img src="/img/shap.png" align=top width="480" hspace="-10" /></figure>

{{< speaker_note >}}
- I trained a SVM classifier using 12 features under 3 categories: demographic (including age and sex), clinical (including top 4 chronic diseases and symptoms), as well as medical resources (including beds and doctors per 10 thousand residents for each country).
- The classifier did pretty a good job at classifying outcomes based on these features, as you can see from high F1 scores and AUC. 
- Features contributing the most the outcome are docs_per_10k and age. To sum up, older patients in countries with fewer doctors are at higher risk.
{{< /speaker_note >}}

---

## Web App

Deployed the trained classifier as a [Heroku web app](https://covid19-risk.herokuapp.com) → take user input to make new predictions

<iframe frameborder="0" width="100%" height="500pt" src="https://covid19-risk.herokuapp.com/"></iframe>

{{< speaker_note >}}
- Finally, I deployed the trained classifier as a web app using Flask + Heroku. 
- The app is embedded in my presentation so you can try it for yourself!
- All you need is to answer a few questions and hit submit, then you can see your probability of death if you get COVID-19.
{{< /speaker_note >}}

---

## Extending this work at TDI

<ul>
{{% fragment %}}<li><b>Retrain and re-deploy model</b> online as more patient data becomes available</li>{{% /fragment %}}
{{% fragment %}}<li>Incorporate <b>state- or county-level data</b> on resource shortages, stay-at-home policies, population density, etc. to make finer predictions </li>{{% /fragment %}}
{{% fragment %}}<li>Predict mortality risk of other diseases.</li>{{% /fragment %}}
</ul>

{{< speaker_note >}}
I plan to extend this work at TDI in several ways:
- First of all, it would be great to retain and redeploy this model as new patient data comes in
- For medical resources, we can add state-level data rather than just country-level data
- We can use the framework to build apps that predict mortality risk of other diseases
{{< /speaker_note >}}

---

# Questions?

[Web App](https://covid19-risk.herokuapp.com/)

[GitHub](https://github.com/Yuan-Meng/COVID-19)

<a href="mailto:yuan_meng@berkeley.edu">Email</a>

{{< speaker_note >}}
- Thanks for listening! I'm happy to answer some questions!
{{< /speaker_note >}}

---

## Contributions

- Older patients are hit harder, but how much harder? **→ Make predictions in a gradient manner** 
- Healthy 80-year-old vs. 20-year-old with chronic diseases? **→ Combine multiple factors**
- **Convenience:** Users can look up their risk on their mobile phone or web browser w/o ML

{{< speaker_note >}}
Yes, we already know age and pre-existing conditions matter, but my project makes unique contributions:
- Although we know older people get hit harder by COVID-19, we don't know how much harder. — This risk predictor can make predictions in a gradient manner.
- Also, we know many factors may contribute to death but what if they contradict each other? For instance, who's at higher risk, a healthy 80-year-old or a 20-year-old with chronic diseases? — This predictor can combine multiple factors into a single prediction.
{{< /speaker_note >}}

---
