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
- At The Data Incubator (TDI), I plan to to build a COVID-19 risk predictor. 
{{< /speaker_note >}}

---

# If I get COVID-19, will I survive or die? 

{{< speaker_note >}}
- The end product will be a web app that predicts users mortality risk if they contract COVID-19.
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
- (As expected, the US now has most patients. Actually, about half of patients are under 48. Most survived.)
{{< /speaker_note >}}

---

## Classifier


- **Features:** Trained an SVM classifier on 12 features (demographic: 2, clinical: 8, medical resources: 2)
- **Performance:** F1 score = .91, AUC = .95 in test; F1 score = .92, AUC = .91 in full dataset

<figure><img src="/img/evaluation.png" align=top width="650" hspace="-10" /></figure>

{{< speaker_note >}}
- I trained a SVM classifier using 12 features under 3 categories: demographic (including age and sex), clinical (including top 4 chronic diseases and symptoms), as well as medical resources (including beds and doctors per 10 thousand residents for each country).
- The classifier did pretty a good job at classifying outcomes based on these features, as you can see from metrics like F1 scores and AUC.
{{< /speaker_note >}}

---

## Web App

Deployed the trained classifier as a [Heroku web app](https://covid19-risk.herokuapp.com) → take user input to make new predictions

<iframe frameborder="0" width="100%" height="500pt" src="https://covid19-risk.herokuapp.com/"></iframe>

{{< speaker_note >}}
- Finally, I deployed the trained classifier as a web app using Flask + Heroku. 
- The app is embedded in my presentation so you can try it for yourself!
- Basically, after answering a few questions, it returns your probability of death if you get COVID-19.
{{< /speaker_note >}}

---

## Extending this work at TDI

<ul>
{{% fragment %}}<li><b>Retrain and re-deploy model</b> online as more patient data becomes available</li>{{% /fragment %}}
{{% fragment %}}<li>Incorporate <b>state- or county-level data</b> on resource shortages, stay-at-home policies, population density, etc. to make finer predictions </li>{{% /fragment %}}
{{% fragment %}}<li>Create a more versatile app that allows users to <b>select models and features</b> to use</li>{{% /fragment %}}
</ul>

{{< speaker_note >}}
I plan to extend this work at TDI in several ways:
- First of all, it would be great to retain and redeploy this model as new patient data comes in.
- For medical resources, we can add county-level data rather than just country-level data.
- It's a bonus if users can choose which models and features to use to make prediction. 
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
