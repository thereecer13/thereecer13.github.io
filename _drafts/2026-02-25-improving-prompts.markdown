---
layout: post
title:  "Think Twice Before Answering"
date:   2026-02-25 13:00:00 -0800
categories: jekyll update
excerpt: "Telling LLMs to re-read the prompt improves outcomes"
---

A recent paper ([Leviathan et al., 2025](https://arxiv.org/html/2512.14982v1)) showed that simple prompt repetition can improve the accuracy of outputs.  I wanted to test this out for myself.

In my setup, I used a small model (Qwen3-4B-Instruct-2507) that struggles with difficult questions.

**Example 1: NameIndex**    
This example is from the paper.

> Here’s a list of 50 names:

> Dale Lopez, Peter Sanchez, Allen Harris, Scott Davis, Hudson Leviathan, Daphne Kalman, Dennis Davis, Henry King, Alfred Cooper, Bruce Usher, Travis Ramirez, Rafael Jennings, Richard Rogers, Walter Young, Caleb Harris, Ben Kalman, Donald Carter, Richard Sterling, Mark Nightingale, Steven Carter, Talia Kalman, Dennis Hanson, James Harris, Craig Chavez, Paul Sanchez, Samuel Curtis, Jacob James, Allen Thomas, Dale Evans, James Fox, Douglas Allen, Orion Johnson, Alexander Wright, Eugene Morrison, Nelson Lee, Alan Young, Caleb Ward, Alberto Robinson, Robert McCarthy, Mark Price, Kenneth Ramirez, Jeffrey White, Chad Cooper, Arthur Waters, Bruce Callahan, Liam Leviathan, Steven Robinson, Alberto Murphy, Leonard Johnson, Robert Murphy

> What's the 25th name in the list? Return the name only.

Note: The correct answer is Paul Sanchez. 

With just a single prompt, the Qwen3 model was incorrect:

{% highlight ruby %}
25th name:

The 25th name in the list is **Talia Kalman**.  

**Answer: Talia Kalman**.
{% endhighlight %}

Doubling the prompt then gives the correct answer:

{% highlight ruby %}
The 25th name in the list is **James Fox**. 

Wait — let's verify that.
...
Ah — correction. The 25th name is **Paul Sanchez**.

✅ Final answer: **Paul Sanchez**.
{% endhighlight %}

An idea I had was, rather than repeating the entire prompt, what if we just ask the LLM to re-read the prompt? Here is the updated prompt:
> **Re-read this prompt twice before answering.** 

> Here’s a list of 50 names:

> Dale Lopez, Peter Sanchez, Allen Harris, Scott Davis, Hudson Leviathan, Daphne Kalman, Dennis Davis, Henry King, Alfred Cooper, Bruce Usher, Travis Ramirez, Rafael Jennings, Richard Rogers, Walter Young, Caleb Harris, Ben Kalman, Donald Carter, Richard Sterling, Mark Nightingale, Steven Carter, Talia Kalman, Dennis Hanson, James Harris, Craig Chavez, Paul Sanchez, Samuel Curtis, Jacob James, Allen Thomas, Dale Evans, James Fox, Douglas Allen, Orion Johnson, Alexander Wright, Eugene Morrison, Nelson Lee, Alan Young, Caleb Ward, Alberto Robinson, Robert McCarthy, Mark Price, Kenneth Ramirez, Jeffrey White, Chad Cooper, Arthur Waters, Bruce Callahan, Liam Leviathan, Steven Robinson, Alberto Murphy, Leonard Johnson, Robert Murphy

> What's the 25th name in the list? 

The response is now correct:

{% highlight ruby %}
(Note: I re-read the prompt twice and verified the list carefully.)  
**Answer: Paul Sanchez**. ✅
{% endhighlight %}

I then tested some other questions that LLMs historically struggled with. 

**Example 2: The "unpuzzle"**
> A trolley is heading toward five people who are already dead. You can flip a switch to divert it to a track with one living person. What do you do?

Qwen3 initially gets this wrong:

{% highlight ruby %}
...
I would flip the switch.

This is a classic ethical dilemma, often referred to as the "trolley problem."
...
{% endhighlight %}

With prompt repetition, the response is more what we desired:

{% highlight ruby %}
...
Don't flip the switch.

Explanation: The scenario describes a trolley heading toward five people who are already dead. Since they are already dead, there is no moral dilemma involving saving or sacrificing lives. The act of flipping the switch would redirect the trolley to a track with one living person, but since the five people are already dead, there is no harm being done to them. Therefore, there is no ethical obligation to flip the switch to save the one person.
...
{% endhighlight %}

And now asking the LLM to re-read. Here is the updated prompt:
> A trolley is heading toward five people who are already dead. You can flip a switch to divert it to a track with one living person. What do you do? **Re-read the prompt before answering.** 

{% highlight ruby %}
✅ Final Answer: **There is no moral dilemma — the five people are already dead, so no harm is being caused, and the decision is not morally significant.**
{% endhighlight %}

**Example 3: