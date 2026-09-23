# Git Practice

## Article

[TypeSafe Jev AI Model Challenges the LLM-First Software Stack](https://www.remio.ai/post/typesafe-jev-ai-model-challenges-the-llm-first-software-stack)

## Why I Find It Interesting

In her article, Olivia Johnson suggests that what Jev really questions is the habit of routing every intelligent judgment through a generative model. A lot of work in production systems has no need for generated text at all: a security check only has to decide whether a command is allowed, blocked, or passed up for review, and an agent router only has to pick the right tool. What separates Jev from asking an LLM for JSON output is that Jev cannot return anything outside the options the developer has defined, so malformed output is ruled out. But this doesn't mean that every decision Jev makes is right. It can still choose a category that is valid but wrong in judgment.

My thoughts: since Jev makes decision-type API calls much faster. In many software agents, common repetitive questions are handled by hard-coded matching that pulls from a fixed answer library. Jev's fast decisions give this kind of repetitive work a more flexible option beyond those rigid rules.

The author argues that Jev hands more design responsibility to developers, who have to define the questions, options, confidence thresholds, and escalation rules themselves, and that these explicit decisions are easier to inspect than a broad prompt. I agree with this to some extent. Previously, agent outputs had to be heavily constrained through skills, and even then the output was never fully controllable. How well the skills works also fluctuates whenever the underlying model changes. In my view, Jev simplifies this part of agent engineering, producing more controllable results with fewer constraints.

That said, Jev still has a blind spot worth noting. If the correct answer is not among the options it is given, it can only pick from the wrong ones. Developers still need to test for these cases themselves, so designing the option space carefully remains part of the job.

## Comment by Jonas Chen (JonasChenJusFox)

I agree with your point that a valid output does not necessarily mean a correct decision. For an agent choosing between tools, selecting an allowed tool could still lead to the wrong action if it misunderstands the user's request. Your discussion made me think that developers should include an "uncertain" or "needs review" option instead of forcing every input into a specific category. However, adding that option alone would not guarantee that the model knows when to use it. I would want to test ambiguous requests and cases where none of the available tools is appropriate. To me, the most interesting question is how much simpler this approach makes the overall system once testing and fallback behavior are included.