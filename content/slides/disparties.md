---
title: CogSci20
summary: Slides for my CogSci20 talk.
authors: [Yuan Meng]
tags: []
categories: []
date: "2020-07-19T00:00:00Z"
slides:
  theme: blood
  highlight_style: dracula
---

### How do disparities reproduce themselves?

<!--###### "Ground truth" inference from utility-maximizing agent's sampling behavior--->

[Yuan Meng](mailto:yuan_meng@berkeley.edu) | [Fei Xu](mailto:fei_xu@berkeley.edu)

University of California, Berkeley

{{< speaker_note >}}
- Hi everyone, welcome to my virtual talk! This is Yuan, a graduate student at UC Berkeley. 
- Today I'll be talking about "How do disparities reproduce themselves?", in which I used social learning models to examine why racial disparities are so persistent and potential ways to combat them.
{{< /speaker_note >}}

---

<ul>
	{{% fragment %}}<h4 align="center">May 25, 2020</h4>{{% /fragment %}}
	{{% fragment %}}<a href="https://en.wikipedia.org/wiki/Killing_of_George_Floyd"><center>8 minutes 46 seconds...</center></a>{{% /fragment %}}
	{{% fragment %}}<figure><img src="/img/cogsci/protests.jpg" width="600" align="center"/></figure>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- On May 25th, 2020, George Floyd suffocated to death after a police officer knelt on his neck for 8 minutes 46 seconds.
- His death sparked worldwide protests against racial disparities in the criminal justice system.
{{< /speaker_note >}}

---

<ul>
  {{% fragment %}}<h3 align="center">How can cog sci help end racial disparities?</h3>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- As cognitive scientists, what can we do to help end racial disparities?
{{< /speaker_note >}}

---

<ul>
	{{% fragment %}}<h4 align="center">Let numbers speak?</h4>{{% /fragment %}}
	{{% fragment %}}Will voters petition <b>against</b> three-strikes law?{{% /fragment %}}
	{{% fragment %}}<figure align="center"><img src="/img/cogsci/numbers.png" width="550" /><figcaption align="right">Hetey and Eberhardt (2014)</figcaption></figure>{{% /fragment %}}
	{{% fragment %}}<center>Why not? <b>Black ↔ Crime association</b></center>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- Perhaps if we just show people the extent of disparities, they'd all be longing for change. However, numbers don't speak for themselves.
- White voters exposed to greater racial disparities in prison were even less willing to petition against three-strikes law that led to the over-representation of Black inmates in the first place. 
- Why? Hetey and Eberhardt explained that people may have stereotypes associating Blacks with crime: A Blacker prison made them more fearful of crime so they became more likely to uphold harsh criminal law, leading disparities to reproduce themselves. 
{{< /speaker_note >}}

---

<ul>
  {{% fragment %}}<figure align="center"><img src="/img/cogsci/casino.png" width="550" /></figure>{{% /fragment %}}
  {{% fragment %}}<center>Which machine would you bet your 💰 on?</center>{{% /fragment %}}
  {{% fragment %}}<center>Why?</center>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- If we can get rid of such stereotypes, will disparities disappear?
- Again, it may not be so simple. We argue that disparities can reproduce via pure rational inference.
- Imagine you're at a casino and are told someone is really good. You saw them putting 2 coins into the first machine and 5 into the second. Which one would you bet your money on? If you say the first, is it because you have stereotypes associating it with rewards?
{{< /speaker_note >}}

---

<ul>
  {{% fragment %}}<h3 align="center">Naïve Utility Calculus</h3>{{% /fragment %}}
  {{% fragment %}}<center>We understand others by assuming they choose goals and actions to <b>maximize expected utilities</b> (expected rewards - costs)</center>{{% fragment %}}
  {{% fragment %}}<figure align="center"><img src="/img/cogsci/nuc.png" width="400" /><figcaption align="right">Jara-Ettinger et al. (2016)</figcaption></figure>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- More likely, you're using some sort of "naive utility calculus" to understand this person. 
- If they are knowledgeable about machines' reward rates and try to maximize expected utilities, it only makes sense if the first machine has a higher reward rate than the second.
- When it's your turn, you'll also the previous person's footsteps, thereby reproducing "disparities" without pre-existing stereotypes. In the current study, we want to test if that is what people do in the police scenario. 
{{< /speaker_note >}}

---

#### Experiment 1: Check rates only

{{% fragment %}}<figure align="center"><img src="/img/cogsci/procedure1.png" width="600" /></figure>{{% /fragment %}}

{{< speaker_note >}}
- To simulate police encounters without introducing existing stereotypes, we designed a game called "The Golden Ticket". 
- In this game, a robot chicken lays one egg at a time, which may or may not have a golden ticket. The chicken is an analogy to a social group and eggs members from that group. As a player, your goal is to win golden tickets --- just like a police officer's goal is to catch criminals. To buy an egg, you need to pay a token, which is both costly and limited, just like a police officer's time and energy.  
- Participants were told that player Alex knows each chicken's reward rate, i.e., the probability that it lays an egg with a ticket. Also, Alex is said to spend tokens carefully.
- Alex played a total of 12 chickens, each laying 6 eggs. They decided whether to buy an egg or let it go. After each chicken, participants were asked to estimate the reward rate and decide whether they'd like to buy an egg from this chicken.
- In Experiment 1, Alex didn't open the eggs, so inference can only be based on "check rates", i.e., the probability of Alex buying from a chicken. 
{{< /speaker_note >}}

---

### Model

<ul>
  <li>Expected utility: $U(\mathrm{buy}) = R\cdot\theta- C$</li>
  <li>Check rate: $P(\mathrm{buy}) = \frac{1}{1 + \exp({-U(\mathrm{buy})})}$
</li>
</ul>

<figure align="center"><img src="/img/cogsci/nuc_check.png" width="500" /></figure>

{{< speaker_note >}}
- The expected utility of buying an egg is the expected reward minus the cost. The cost is always the value of the token, $C$. The expected reward depends both on the value of a ticket $R$ and the reward rate $\theta$.
- According to NUC, participants understood Alex's behavior by assuming that the higher the expected utility, the more likely they would buy an egg. The relationship between utility and Alex's check rate $\mu$ is given by this logistic function. 
- Using this model, we can infer the underlying reward rate from Alex's check rate.
{{< /speaker_note >}}

---

### Results 

62 US participants recruited on MTurk 

{{% fragment %}}<figure align="center"><img src="/img/cogsci/exp1.png" width="600" /></figure>{{% /fragment %}}

{{< speaker_note >}}
- Here's the results. 
- The figure on the left shows the reproduction of "disparities": The more eggs Alex bought from a chicken, the more likely participants would also buy from it. 
- The figure on the right suggests that participants inferred chickens' reward rates in pretty much the same way as the NUC model I showed you moments ago.
{{< /speaker_note >}}

---

### How do we break the cycle?

{{< speaker_note >}}
- The question is, how can we break the endless cycle of disparities reproducing themselves?
- A possible solution is to show people the reward rates in the egg samples. 
{{< /speaker_note >}}

---

#### Experiment 2: Check + hit rates

{{% fragment %}}<figure align="center"><img src="/img/cogsci/procedure2.png" width="600" /></figure>{{% /fragment %}}

{{< speaker_note >}}
- Back to police encounters: Seeing that African Americans who are checked by the police are no more likely to commit crimes, will people update their inference?
- We designed a new experiment to find out. In Experiment 2, Alex opened the eggs they bought so participants knew the "reward rates" (or "hit rates") as well, at least in the samples. 
{{< /speaker_note >}}

---

### Models

<figure align="center"><img src="/img/cogsci/models.png" width="500" /></figure>

{{< speaker_note >}}
- Now participants can still rely on check rates, thinking what they saw in the samples were just a fluke.
- Or, they may fully switch to observed hit rates, thinking they are equal to true hit rates in the population.
- Alternatively, participants might combine both pieces of information. If a chicken had a high check rate but a low observed hit rate, then the true hit may be somewhere in the middle.
{{< /speaker_note >}}

---

### Results

67 US participants recruited on MTurk 

{{% fragment %}}<figure align="center"><img src="/img/cogsci/exp2.png" width="600" /></figure>{{% /fragment %}}

{{< speaker_note >}}
- None of the 3 models captured human inference exactly. 
- When check rates were low but hit rates were high, the best performing model is the one that considered both check rates and hit rates.
- When check rates were high but hit rates were low, the hit rate only model was the closet to people's responses. 
- Why is this the case? A possible explanation is that information about hit rate is more salient than information about check rates. 
- In the first 2 scenarios, participants had strong evidence that check rates were low but only weak evidence that hit rates were low so they relied on both pieces of information.
- In the last 4 scenarios, there was strong evidence for both high check rates and low hit rates. In this case, participants relied more on hit rates.
- Of course, this is just one explanation among many. Even though the mechanism is unclear, but providing hit rate information is effective in this case to break the cycle: Participants no longer relied on Alex's behavior to guide their choices.
{{< /speaker_note >}}

---

### Summary 

<ul>
  <li>
      Experiment 1: high check rate → high hit rate
      <ul>
        <li>Potential explanation for why racial disparities are persistent</li>
      </ul>
  </li>
  <li>Experiment 2: people relied more on observed hit rate than check rate to infer true hit rate</li>
      <ul>
        <li>Potential solution to end this viscous cycle</li>
      </ul>
</ul>

{{< speaker_note >}}
- So to sum up, with only check rates available, participants inferred that chickens checked more often have high hit rates.
- When both check rates and observed hit rates are known, participants replied on both and even more heavily on hit rates.
- This first finding provided a possible cognitive explanation of why racial disparities are so persistent. The second provided a potential way to end this vicious cycle.
{{< /speaker_note >}}

---

### What's Next

<ul>
  <li>Social groups as stimuli</li>
  <li>Consensus between agents</li>
</ul>

{{< speaker_note >}}
- All this about racial disparities, we haven't used social groups as stimuli yet. This is what we'll do next. It's possible that we think people are more variable than objects so one should trust observed hit rates less. Alternatively, we may think group members share the same essence so observed hit rates represent what the whole group is like.
- Also, in real life, it's not one officer that targets minorities groups but many officers around the world. It may be more challenging to break free from racial disparities when there's consensus between utility-maximizing agents, which is worth examining next.
{{< /speaker_note >}}

---

# Questions?

Email:[yuan_meng@berkeley.edu](mailto:yuan_meng@berkeley.edu)

GitHub: [github.com/Yuan-Meng/PISG](github.com/Yuan-Meng/PISG)


{{< speaker_note >}}
- Thank you for attending my virtual talk!
- This is still an early step towards this line of research. Questions and feedback are more than welcome! Please feel free to email me or check out the source code. 
- Thank you all!
{{< /speaker_note >}}