---
title: COVID-19 Risk Predictor
summary: 
authors: [Yuan Meng]
tags: []
categories: []
date: "2020-07-23"
slides:
  theme: solarized

---

# Reopen Navigator

Yuan Meng

Capstone @TDI, Jul. 23, 2020

[Code](https://github.com/Yuan-Meng/COVID-19) | [Web App](https://covid19-risk.herokuapp.com/)

{{< speaker_note >}}
- Hi, this is Yuan and this my capstone project at The Data Incubator, "Reopen Navigator".
- It's a web app I designed to help users safely navigate the post-pandemic world after reopening.
{{< /speaker_note >}}

---

<figure><img src="/img/covid/reopen.png" width="800" /></figure>

{{< speaker_note >}}
- Four months into the COVID-19 pandemic, all 50 states in the US have reopened to varying degrees. 
{{< /speaker_note >}}

---

### Reopen = safe for me?

<ul>
  {{% fragment %}}<figure><img src="/img/covid/second_wave.png" align=top width="800" /></figure>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- This is the time that gives us hope and confusions: Our old life is coming back but is it safe?
- What people need right now is information, "Given my medical condition and my local situation, is safe for me to go out or even visit friends?"
- My app is designed to provide personalized information for each user.
{{< /speaker_note >}}

---

### Web App

- **Input:** age, chronic diseases, location, party size
- **Output:** severity, risk factors, infection risk
<iframe frameborder="0" width="100%" height="500pt" src="https://covid19-risk.herokuapp.com/"></iframe>

{{< speaker_note >}}
- Users first enters their age, whether they have chronic diseases releated to COVID-19 mortality, which state they live in, and if they wish to visit friends, what's the intended party size.
- Then based on the input, the app will first tell the user how likely they may get COVID-19, if they get it, how likely they may experience severe outcomes, and how each risk factor contributes to that outcome.
{{< /speaker_note >}}

---

### Use cases

- **Own risk:** "I'm a 60-year-old California resident with diabetes. Can I safely go out by myself?"
- **Social contacts:**  "Should I go kayaking with 3 friends this weekend?"
- **Government**: Send warnings to at-risk populations; adjust safe "social bubble" size

{{< speaker_note >}}
- You can use this app to estimate your own risk. If you want to visit friends, you can evaluate their risks. Local governments can also use it to send out warnings to at-risk populations and adjust the safe party size for the local population.
{{< /speaker_note >}}

---

# Thank you!

{{< speaker_note >}}
- Life has to continue and I hope my app can help people do so safely.
- Thank you all for listening!
{{< /speaker_note >}}

---

### Under the hood

<figure><img src="/img/covid/data.png" width="800" /></figure>

{{< speaker_note >}}
- If you're interested, here's what it looks like under the hood.
- To predict outcome severity, I used a clinical dataset with 300 thousand COVID-19 patients and their treatment outcomes.
- To predict infection risk, I used each state's COVID-19 testing data, assuming that the proability of a random person carrying the coronavirous is equal to the percentage of positive cases out of all people tested.
{{< /speaker_note >}}