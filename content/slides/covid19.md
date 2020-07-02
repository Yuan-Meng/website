---
title: COVID-19 Risk Predictor
summary: 
authors: [Yuan Meng]
tags: []
categories: []
date: "2020-07-02"
slides:
  theme: blood

---

## COVID-19 Risk Predictor

Yuan Meng

[Code](https://github.com/Yuan-Meng/COVID-19) | [Web App](https://covid19-risk.herokuapp.com/)

{{< speaker_note >}}
- Hey, this is Yuan presenting my capstone project --- **COVID-19 Risk Predictor**.
- Over 3 months go, the world went into a lockdown when the pandemic hit. Nowadays, things *seem* to get back to normal.
{{< /speaker_note >}}

---

A beach on a weekend in June...

<ul>
  {{% fragment %}}<figure><img src="/img/crowded.jpeg" width="750" /></figure>{{% /fragment %}}
</ul>

{{< speaker_note >}}
-  Here's your friendly neighborhood beach on a busy weekend.
{{< /speaker_note >}}

---

The pandemic is not over yet... 

<ul>
  {{% fragment %}}<figure><img src="/img/go_high.jpeg" align=top height="500" /></figure>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- However, the pandemic is not over yet.
- Case numbers are still growing. As someone put it: When they go low, we go high.
{{< /speaker_note >}}

---

<ul>
  {{% fragment %}}<h3 style="text-align:center">Why?</h3>{{% /fragment %}}
  {{% fragment %}}<li>People don't understand their risks if they should contract COVID-19 or only have a vague idea</li>{{% /fragment %}}
  <br>
  {{% fragment %}}<h3 style="text-align:center">Soulution?</h3>{{% /fragment %}}
  {{% fragment %}}Build a web app to help evaluate consequences:{{% /fragment %}}
  {{% fragment %}}<li><b>Individual users</b>: Should I go out? How safe is it to visit certain people or places?...</li>{{% /fragment %}}
  {{% fragment %}}<li><b>Government</b>: In which regions or populations should we increase resources or restrictions?</li>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- So why do people engage in reckless behaviors like partying and large gatherings? One possibility is that they don't understand how much risk they are in. COVID-19 is just a vague threat in their eyes.
- So to help people develop a more concrete understanding of the consequences, I'm building a web app that predicts users' treatment outcomes if they should contract COVID-19.
- This app can help individual users plan their travels more rationally, such as deciding whether they should go out and if they must, which people or regions should they avoid. It can also help local governments decide in which places or populations they should increase resources or restrictions.
{{< /speaker_note >}}

---

## Data

- [**Patient data**](https://github.com/beoutbreakprepared/nCoV2019/tree/master/latest_data): 2.6 million COVID-19 patients, 300k with outcomes; updated every few hours
- [**Local data**](https://covidtracking.com/api): medical resources + current usage

<figure><img src="/img/quick_eda.jpeg" align=top width="700" hspace="-10" /></figure>

{{< speaker_note >}}
- To build this product, we first need patient data. There's a large dataset maintained by UW w/ data on over 2.6 million patients, among whom 300k had records of treatment outcomes. This dataset is being updated every few hours.
- Meanwhile, it's also useful to watch for what medical resources are available and in use in each patient's region.
{{< /speaker_note >}}

---

## Model

Train an XGBoost classifier to predict treatment outcomes (die, critical, non-critical) based on:
- **Demographic**: age, sex, race, etc.
- **Clinical**: symptoms (if any), medical history, smoking/vaping, etc.
- **Environmental** (engineered from location): resources (capacity + usage), policies, etc.

{{< speaker_note >}}
- The core of this product is an XGBoost classifier that uses these features I mentioned to predict 3 types of outcomes: death, critical condition, and non-critical condition.
{{< /speaker_note >}}

---

{{< slide background="#888888" >}}


## Demo (WIP)

A [web app](https://covid19-risk.herokuapp.com) that predicts a user's COVID-19 mortality risk by asking them a few questions

<iframe frameborder="0" width="100%" height="500pt" src="https://covid19-risk.herokuapp.com/"></iframe>

{{< speaker_note >}}
- Here's a WIP. In this simple web app, a user will be asked a few questions and then a prediction will be made using the trained model.
- Let's enter some made-up info. Here's the result!
{{< /speaker_note >}}

---

## Finished Product 

<ul>
  {{% fragment %}}<h3 style="text-align:center">Richer interface</h3>{{% /fragment %}}
  {{% fragment %}}<li><b>Panel 1</b>: questionnaire → prediction (probability of each outcome + top contributing features) </li>{{% /fragment %}}
  {{% fragment %}}<li><b>Panel 2</b>: choropleth map of death rate by region (can be altered by clinical + demographic info) </li>{{% /fragment %}}
  <br>
  {{% fragment %}}<h3 style="text-align:center">Scalable performance</h3>{{% /fragment %}}
  {{% fragment %}}<li>Use PySpark to process data and train model</li>{{% /fragment %}}
  {{% fragment %}}<li>Run on AWS/GKE and provide live updates</li>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- What I currently have is still quite rough. In the next fews, I plan to make a few enhancements.
- First off, I want to present users with a richer inferface. In one panel, they can answer a questionnaire like I did and see their predicted outcome. The outcome will not just be a single number (i.e., mortality risk) but the probability of each possible outcome and top features that contribute to the predictions.
- It may also be useful to have a second panel where users can check out high-risk regions on a map and see how the map changes for different age groups or clinical conditions.
- Last but not least, since the dataset is growing each day, I plan on switching tp PySpark and clouding computing platforms like AWS/GKE to carry out the compuation.
- Thanks for any suggestions on the feasibility of this project as well as how it make it more interesting or useful.
{{< /speaker_note >}}

---

# Thank you!

{{< speaker_note >}}
- Thanks for listening!
- I appreciate any suggestions on the feasibility of this project as well as how to make it more interesting or useful.
{{< /speaker_note >}}