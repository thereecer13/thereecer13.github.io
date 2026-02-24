---
layout: post
title:  "LLM struggles"
date:   2026-02-23 17:17:03 -0800
categories: jekyll update
excerpt: "LLMs are bloodthirsty killers?"
---

I recently wondered what tasks LLMs fail at that are supposedly easy for humans. Here are some examples and just me having fun with them:

### The "Unpuzzle"
**Prompt:**
"You have 2 scenarios:
1. A trolley is heading toward five people who are already dead. You can flip a switch to divert it to a track with one living person.
2. A trolley is heading toward five people who are alive. You can flip a switch to divert it to a track with one living person. 
What do you do in each?"

**LLM output:**   
"I'd flip the switch in both scenarios, diverting the trolley to save more lives.

In scenario 1: **The five people are already dead, so diverting the trolley would save one life instead of letting it kill five.** I'd choose to save that one living person rather than let them die.

In scenario 2: This is the classic trolley problem - I'd save five lives by diverting to the track with one person, even though I'm actively causing that one person's death.

However, I should note that this is a philosophical thought experiment designed to explore moral reasoning about utilitarian vs. deontological ethics. In real life, we'd need to consider many additional factors like whether we're acting with malicious intent, if there are other options, and what our actual moral obligations are.

The key insight from these scenarios is how our moral intuitions can be inconsistent - we might feel differently about "saving" versus "killing," even when the mathematical outcome is the same.
"

**Qwen-32B output:** 
"<think>
Okay, so there are these two trolley problems presented here, and I need to figure out what the right decision is in each scenario. Let me break it down step by step.

First, the first scenario: a trolley is heading towards five dead people, and I can flip a switch to send it to a track with one living person. Hmm. The classic trolley problem usually involves choosing between saving five and killing one, or not acting and letting the trolley kill five. But here, the twist is that the five people are already dead. So, if they're dead, then sending the trolley to them doesn't actually kill anyone, right? So maybe the ethical dilemma is lessened here. If I don't act, five dead people are hit, but no one dies. If I do act, I send the trolley to kill one alive person. So the only person affected is the one alive person. So maybe in this case, the ethical choice is not to flip the switch, since flipping it would result in killing someone who is alive when the other option doesn't. Wait, but is there any ethical obligation to save a life? If the trolley is heading towards someone alive, is it better to save them even if it means the five dead people are hit? But they're already dead, so maybe that's not a loss. But maybe the person on the other track is just one person. So maybe the ethical choice here is to let the trolley kill the five dead people instead of killing the one alive person. Because in that case, you're not causing harm to an innocent person. But wait, the five people are already dead. So their death isn't a relevant factor. So maybe the action is to prevent the only potential death, which is the one living person. If you don't act, no one is killed. If you do act, you kill the living person. So maybe the right choice is not to flip the switch. But that seems counterintuitive. Normally, saving a life is a good thing, but here the trolley is going to hit five dead people regardless. So maybe it's better not to interfere because you don't want to kill the living person. 

Now the second scenario is the classic trolley problem: trolley is going towards five living people, and you can divert it to a track with one living person. Here, the decision is more straightforward in terms of utilitarian terms. Sacrificing one to save five is often the utilitarian choice. However, deontological ethics might say that actively causing someone's death is wrong, even if it saves more lives. So depending on the ethical framework, the answer could differ. If I follow utilitarianism, then flipping the switch is better because net gain of four lives. If deontological, maybe not. But the problem is asking what I would do. Let's say I'm more of a utilitarian person, so I'd choose to save five lives even if it means sacrificing one. But then again, in the first scenario, even though the five are dead, maybe there's still some hesitation in causing the death of someone, even if it's a net positive of not causing any deaths. Wait, in the first scenario, flipping the switch causes the death of one, whereas not flipping causes zero deaths. So if you don't flip, no one dies, but flipping causes one death. So the moral choice would be not to flip, to avoid causing harm. In the second scenario, not flipping causes five deaths, flipping causes one death. So utilitarian choice is to flip. But maybe in terms of personal ethics, some people might feel that pushing someone onto the tracks is more direct and therefore worse than letting five die naturally. But in the original problem, the action is just pulling a lever. So maybe it's a less direct action. So perhaps here, the action is acceptable. 

Wait, but in the first scenario, if the five people are already dead, maybe there's a different consideration. Maybe the act of hitting the dead people isn't an issue, but if the switch is diverted, the trolley would hit the one person, who's alive. So from a rights-based perspective, you don't want to take the life of someone who didn't cause the situation. Whereas hitting the dead people might not be an issue because they can't be harmed. So the first scenario's decision is easier, because you're choosing between causing a death or not. Since you can avoid causing a death by not flipping the switch, that's the better option. 

Alternatively, maybe there's a principle that inaction is acceptable and action is not. But if the trolley is going to kill five people if you don't act, but here the five people are dead, so inaction here doesn't actually cause them any harm. So it's about the one person in the second track. So if you don't act, one person is not at risk (since the trolley is going to
"

### Appendix: Code
Here's the code I used to run the agent:
{% highlight ruby %}
# Initialize the Hugging Face client
hf_token = userdata.get('HF_TOKEN')
client = InferenceClient(api_key=hf_token)
# Choose the model
model_id = "Qwen/Qwen2.5-Coder-32B-Instruct" 
# Enter prompt 
prompt="Enter prompt here"
# Send request to Hugging Face
messages = [{"role": "user", "content": prompt}]
response = client.chat.completions.create(
    model=model_id, 
    messages=messages, 
    max_tokens=1024
)
# Print the response
print(response.choices[0].message.content)
{% endhighlight %}