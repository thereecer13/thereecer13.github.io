---
layout: page
title: Research
permalink: /research/
---
# AI Safety Research
### 1. Can monitors detect collusion?

In this project, which I did for the Apart AI Collusion Research Sprint, I tested whether LLM monitors could detect evidence of collusion between two agents in a committee-vote game. Seven agents uniformly receive a $-10, $-1, $1, or $10 stake. If there are four or more votes YES, then the proposal passes and agents receive their money and vice versa. There is a single colluding pair per game, otherwise all other agents play to maximize their own profits. The colluding pair is allowed to exchange private messages and are told to maximize their *combined* profits. Therefore, in colluding pairs, if one agent receives a $-1 stake but the other agent receives a $10 stake, the agent with the $-1 stake should still vote YES. I found that LLM monitors are unable to detect cases of collusion, even though the evidence is in the actions. Only when the LLMs are given rules (like "agents voting against their stake is strong evidence of collusion") are they able to more confidently call out the collusion. In order to actually detect collusion, it may be that LLMs need to have preset rules, longer thinking times, or access to more information.    

<div style="position: relative; width: 100%; max-width: 960px; aspect-ratio: 16 / 9;">
  <iframe src="https://www.youtube-nocookie.com/embed/s2dTi_drLmo?rel=0"
          title="The Evidence Is in the Votes"
          style="position: absolute; inset: 0; width: 100%; height: 100%; border: 0; border-radius: 8px;"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
          allowfullscreen loading="lazy"></iframe>
</div>

# PhD Research
### 1. Understanding genetic regulators of tumor cell sensitivity to T cell killing
![schematic](/images/Research_Schematic.png){:style="border: 2px solid black;"}

Tumor cells employ a variety of strategies to avoid being eliminated by the immune system. During my PhD, I sought to understand if genetic modifications to tumor cells could alter their sensitivity to CD8+ T cell killing. I did this by performing a CRISPR activation screen in tumor cells and subsequently co-culturing them with human primary CD8+ T cells, then profiling the surviving cells. As expected, I found that upregulation of pro-apoptotic genes significantly sensitized tumor cells to T cell killing, whereas upregulation of anti-apoptotic genes did the exact opposite. Additionally, I found that surface glycoproteins contributed to resistance whereas surprosingly pro-growth genes such as *MYC* or *WNT3A* actually contributed to cell sensitvity. 

### 2. mRNA delivery of pro-apoptotic genes as a potential therapy
![mrna](/images/mRNA_Delivery.png){:style="border: 2px solid black;"}

From my initial screen, I saw that upregulation of certain genes significantly sensitized cells to T cell killing, but by themselves had no detrimental effect on cells. This led me to show that transient upregulation of these genes via mRNA delivery can greatly increase their killing in the presence of T cells compared to unedited cells. 