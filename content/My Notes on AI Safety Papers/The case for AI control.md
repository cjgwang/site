---
title: The case for AI control and criticisms
draft: false
tags:
  - control
  - ai_safety
---
In this blogpost I will present the basic argument for the AI control agenda. This is the most clearly presented by Ryan Greenblatt and Buck Shlegeris in "[The case for ensuring that powerful AIs are controlled](https://www.alignmentforum.org/posts/kcKrE9mzEHrdqtDpE/the-case-for-ensuring-that-powerful-ais-are-controlled)", "[AI Control: Improving Safety Despite Intentional Subversion](https://arxiv.org/abs/2312.06942)", and "[Catching AIs red-handed](https://www.alignmentforum.org/posts/i2nmBfCXnadeGmhzW/catching-ais-red-handed)". I will also evaluate critiques of the AI Control Agenda, such as those by [John Wentworth](https://www.lesswrong.com/posts/8wBN8cdNAv3c7vt6p/the-case-against-ai-control-research).

AI control is the area of AI safety that mitigates the safety risks from deceptively misaligned, scheming AI (although some argue that scheming might occur naturally in aligned AI). Scheming is the behaviour in which models intentionally choose actions that maximise the likelihood that they eventually seize power. This is separate from alignment work, which tries to ensure model's aren't scheming as opposed to prevent harm from scheming models. 

Here are some ways that scheming AI could pose as an existential risk:
- An AI manipulates a high-clearance OpenAI engineer to deploy it before performing robust safety checks
- A powerful AI hacks into the AI lab datacenters and gets control of its own training
- A model self-exfiltrates its weights

Strong claim: I think that the case for AI control is that the ROI on safety outcomes from doing control research as at least as high as doing alignment research, specifically for scheming models.

Weak(er) claim: Ryan and Buck specifically make the claim that AI labs could, with substantial effort, implement better control techniques that substantially reduce risk from early transformative AI. This is, in my opinion, a easy claim to accept. 

Here are some reasons why you should accept the weaker claim:
1. Evaluating control is far easier than evaluating alignment.
2. It is likely that control can be achieved for early transformative AIs.

You might be more convinced by reasons and arguments I present in this post if: 
- You have a higher p(fast takeoff) and a lower p(gradual disempowerment) -> you might weight the importance of preventing misalignment in early transformative AI more than potentially solving misalignment in the future.
- You are more pessimistic about alignment going well (either because it won't happen by default and/or because it will be very hard to achieve), and thus think we should have better control as a last-ditch safety net.

**Robust control is easier than robust alignment.** 
Ryan and Buck introduce an approach using control evaluations on the protocol (a plan for training, evaluation, and deployment).

Step 1: The red team searches for attacks, which are strategies that an untrusted model can use to cause an undesirable outcome. 
Step 2: The red team trains the model to implement the attack strategy. 
Step 3: The blue team tries to catch the AIs red-handed and subvert the attack.

This relies on the capability of the red team and the blue team. The red team needs to be at least as good as a misaligned, scheming model, and the blue team needs to be at least as good as our current control/safety systems. 

The control evaluation is iterated until an untrusted model is caught red-handed in its scheming attempts, and the model is deemed safe by estimating the probability that an undesirable outcome would occur if the model used the attack strategy. 

Some uncertainties I have with this protocol:
- Sandbagging (afaik). The model might pretend to implement the attack strategy and get caught red-handed intentionally, but when deployed be able to successfully avoid detection. 
- Working with superhuman AI. I am less confident about the trusted-untrusted model control protocol once both the trusted and the untrusted model has capabilities far above humans, and other scalable oversight problems. 
	- This concern is supported by some other people. I think this comment by Lukas Finnveden is a good set up to explain it: 
	> Let's assume that an AI lab is in a fast-paced, rapidly changing state of affairs. (As you might expect during a moderately fast takeoff.) If an AI then gets to do the equivalent of 3 months of thinking, it could use that to do notably more serial thinking about how to exploit the current situation than any human has done (because some important features of the current situation is less than 3 months old: e.g. you had to switch to an importantly different programming language, or some different type of communication protocol between AIs, or change your AI safety research paradigm in a way you didn't expect). 

This strategy proposal seems a lot more tractable to me than alignment (due to alignment faking, etc), and I think this is enough to prove that ROI in control is at least as high as ROI in alignment. 

**We might be able to control early transformative AI.** 

This boils down to the argument that without wildly superhuman skills in problematic domains (e.g. creating bioweapons, manipulation), evading robust control techniques is probably difficult. The blogpost goes into a lot of detail to justify this, but I think this makes a lot of sense even intuitively.  

The end picture is a bit blurry to me here: for how long will we have controllable and tranformatively useful AI? Obviously, we want to delay the "loss of control" as much as possible unless we have very significant, robust evidence that doing so will not lead to catastrophic risks, but it is not clear whether AI control is an end goal as much as it is a temporary mitigation technique. (This does not take away from the fact that buying time is extremely good.)

**There are some clear criticisms to this.** 

I think that the biggest issue is that AI control cares about (a) intentional scheming in (b) early transformatively useful models. 

John Wentworth thinks that this is a "relatively small slice of the AI x-risk probability mass". I agree with him that intentional scheming in early models is probably not the biggest thing we should be worried about. 

I think that if you believe AI control is not negligibly small (<5%) of the AI x-risk probability mass, you should still think that AI control still seems more tractable than the hard alignment problem and I think John should believe in the Weak Claim.

Either way, John argues that the median way someone dies in the case of AGI is not by scheming, and that control research might suffer from generality/scaling issues as much as alignment. I don't have too strong opinions about these, I think they are probably correct, and I encourage you to read his blogpost. 