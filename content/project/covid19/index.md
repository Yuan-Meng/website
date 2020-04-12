---
title: COVID-19 Risk Predictor
summary: Web application predicting **personal COVID-19 mortality risk** based on user-inputted **clinical** (preconditions and symptoms) and **demographic** (age and sex) information.
tags:
- Machine Learning
- Web App
- COVID-19
- Predictive Modeling
- Python
date: "2020-04-10T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: SARS-nCoV-2 virus
  focal_point: Smart

links:
- icon: github
  icon_pack: fab
  name: GitHub
  url: https://github.com/Yuan-Meng/COVID-19
- icon: calculator
  icon_pack: fas
  name: Web App
  url: https://covid19-risk.herokuapp.com/ 
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: "example-slides"
---

> If I get COVID-19, will I survive or die?

As the pandemic glooms over the world, this question might have crossed your mind. We probably all heard that COVID-19 hits older people harder than younger people. But how much harder? Not just age, many factors such as a patient's preconditions, whether they have symptoms, how severe their symptoms are, etc. all seem to play a role on treatment outcomes. It's hard to say who's at higher mortality risk, an asymptomatic 70-year-old with no preconditions or a 20-year-old with asthma and pneumonia?

None one knows for sure. Even the best-kept [patient-level dataset](https://github.com/beoutbreakprepared/nCoV2019/tree/master/latest_data) only has 1,005 patients with known outcomes out of 266,874 (as of April 12th, 12:08 AM PDT). So even our best predictions will be based on small and potentially biased data (e.g., death is more newsworthy and better documented). That said, an "educated guess" may still be better than a shot in the dark. It may help at-risk populations think twice before going out and aid health professionals in evaluating mortality risk of tricky cases (e.g., young people with preconditions). 

To this end, I built a simple [web app](https://covid19-risk.herokuapp.com/) that asks people simple questions about their age, biological sex, preconditions, and potential symptoms to evaluate their mortality risk. The heart of the app is an SVM classifier that I trained on these features in the aforementioned 1,005 patients (my [code](https://github.com/Yuan-Meng/COVID-19)). The interface now looks pretty bare bone. Feel free to play around but keep in mind of potential biases and high uncertainty in any predictions!

{{< figure src="/img/webapp.png" width="700">}}

The next step is to obtain external data (e.g., local public health policies and medical resources) that may help the classifier make more accurate and personal predictions.