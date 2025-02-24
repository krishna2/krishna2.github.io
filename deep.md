# Shallow to Deep  

You are probably wondering what's all the news (fuss?) with OpenAI or DeepSeek. Or maybe you noticed the 5% drop in your portfolio (or 10% drop in your $nvda wallstreetbets based trade). Everyone and their cousin is talking about model this, parameter that, distillation this and RL that.

Much much wiser smarter folks have written about all this and go through that for the full details. I will add all the links below.

If you are technical and working in the field of ML/AI, then too this post is likely not for you.

This post was written around 28th of January 2025.

## What the bleep happened?

Here's the news in brief: Last Wednesday, a Chinese company called DeepSeek released a model called R1 - which blew out the performance of all other large models (such as OpenAI's ChatGPT / O1, Anthropic's Claude, Google's Gemini, Meta's Llama ... ). That a model can beat these four giants itself would be big news.

But just to seemingly add insult to injury, the company is a small company (a non-profit arm of a hedge fund), and it is from China and they claimed they trained this model on a budget of $6M.

## Really? Why is that cool?

If you didn't fully catch the drift, that's like one puny David beating Four Goliaths at the same time ... while being blindfolded and with one hand tied to his back.

## Why are they being from China a problem?

Well, the obvious (silly?) answer is that the USA just likes the USA and to quote Gavin Belson from Silicon Valley (HBO), "I don't want to live in a world where I am not the one responsible for world peace". 

But more so because the USA has imposed trade restrictions on GPU chips (which are needed to train such large models - and generally, we are talking more chips than that's consumed during Superbowl). This company (deepseek) is supposed to have done this feat with 2k chips. (fun tidbits : there are some news sources that claim that they have access to over 50,000 chips and further there is also news that 25% of Nvidia's revenue is from Singapore and the claim that somehow the chips found their way from Singapore to China).

## Why is them being tiny a problem?

The conventional wisdom(?) has been that bigger is better. Just on Friday, we saw the President and Sam Altman along with Larry Elison and Japan's Softbank's Masayoshi Son, announce Project Stargate (whatever) needs $500B in capital (yes, that 5 followed by 11 zeroes). 

So obviously when someone else releases a better model for 5 million (5 followed by only 6 zeroes), it is going to be problemooooo (so there, the five zeroes moved from the budget to problem).

## Wait? How?

The further rub in the wound is that the deepseek team innovated their way out of the gpu-restrictions and budget amount.

As they say: Necessity is the mother of invention and constraints force one to come up with cool ways out.

## What did they beat?

The current best models are roughly:

1. OpenAI's O1 and O3 (these followed their GPT4). These are at the top of various prestigious benchmarks. These are their reasoning models.

2. Anthropic's Claude (Sonnet 3.5): This is an amazing model - it is widely claimed to be very good for coding.

3. Google DeepMind's Gemini: They have between Flash and Pro sizes and versions 1.5 and 2.0, some of the best models out there. They top the LMSys (benchmarks arena which has a cool elo rating) and they are very good for multimodality.

4. Meta's Llama: while they don't top any leaderboard as such, they are open-source models. Anyone can copy them and use them on their machines. And these play an important role in the deepseek story.

## What's a model?

It's just a big list of numbers. Floating point numbers. Matrices of Numbers. They are arranged in a certain way. Think of them as a very very big massive equation. (apologize for the multiple superlatives -- will explain why in a bit). They take input numbers, do something with them and output lots of numbers.

Whatever you give as an input : a text message, a question, an image, a video .... all of them are but numbers.
Whatever is output by the model as numbers are then converted back to a text message, your answer, an image ... etc.

## What's with the model size?

Model sizes / parameters: When they say something is a 3b model or 7b model or some big numbers such as Llama's 405B model or now DeepSeek's 601B model, that indicates the number of numbers.

The Llama 401b model has 401 billion floating point numbers.

Deepseek's largest model has 601 billion numbers.

## So they just created a bigger better model? How?

The Deepseek team invented (or used) some very cool tricks. Just for kicks, here are a few of them. 

1. They came up with some gpu (chip) tricks to do fast data transfer and calculations.
2. They came up with a way to split the model to many experts (called mixture of experts) so one big 601b model has say 15-20 models embedded within it). This way at any one time, only a fraction of the model needs to be loaded to memory.
3. Predict multiple outputs at the same time.
4. Use a lesser (fp8 as opposed to the usual 32 or more conventionally bfloat16 in ML) precision of the floating point numbers.
5. They used Distillation techniques - which is making one smaller model (called the student) learn from a larger more accurate model (called teacher). Thus the teacher is big and slow but more accurate while the student is small and fast but eventually learns to be sufficiently accurate over time.
6. Cool ways to cache various intermediate values (Q, K, V -> Query, key, value that are used by the Tranformer's Attention mechanism).
7. And above all, my most favorite of them all, Reinforcement Learning!

## Reinforcing what again?

Reinforcement Learning is a cool technique method in which a system can be made to train by itself. The prerequisite is that the knowledge, the methods/process, and the goals are well known. Especially the outcome should be well defined. For e.g., this is how computers get good at games, such as Atari games, Chess and even Go.
The model plays with itself (untiringly, millions and millions of times) and tries to "learn" what's the best way to a high (winning) score.

## What's the normal of learning then?

As you will recall, supervised learning (supervised fine-tuning (SFT)) is the typical way. This is so called because there is a data set that has been meticulously (supposed to be) labeled by human experts and the models learn how to behave like the human judges. They further "learn" how to generalize to any input rather than just memorize the specific inputs that it has been trained on.

## How about unsupervised learning?

When the modality was images, it had to be trained with human labeled datasets.
But the big reason why text / language models suddenly took over is that we figured out a way to train in an unsupervised manner. How so? Because we humans have created tons and tons of text (language material) and we all follow language grammar and rules and conventions (or at least we are supposed to). (never mind, there are good ways to figure out good and bad and throw away the nonsensical).

The big breakthrough was to formulate the problem as a "next word prediction" problem and make the model learn what is going to come next.

Long long .... ago

in a kingdom far far .... away

once upon a ..... time

These are trivial examples but as you can see, language is *predictable*. Even if not the exact word, a possible set of words.

## So why is Reinforcement Learning (RL) now suddenly cool?

Please take a guess (in your mind) how large the datasets are that are used for the large language models. These are in the order of trillions of tokens (you can roughly say words too. Tokens are just words split in some convenient manner - according to some algorithm). All the public internet data (and many private data too! hey hey) has been already used up.

Models need more data.

There are some methods such as creating synthetic data - but this is hard (unless there is careful supervision and high quality set to start with and clear goals and correct scope). If you are not careful, it will be a case of - garbage in, garbage out.

With reinforcement learning, the models can "self play" and create various possibilities.

## Is that all?

Noooooo ... I simplified it - absolutely no disrespect to the amazing research all along the way. To give a sample, here are a few of them.

Along with reinforcement learning, there have been a few cool hacks that have already helped models learn along the way.

Extra credit reading for the curious:

1. Prompts - of course, you might've heard about prompt engineering and all that ... this is a way of clearly explaining what you want.
2. Retrieval Augmentation : providing correct resources (instead of asking to search the library, you are giving the model 3 books and telling it that the answer is just in these books)
3. In context learning: Providing some examples of what is correct, what is wrong, how the answer should be and providing rubrics of how you would evaluate the answer. (this is also part of the prompt).
4. Instruction tuning: Rather than just making it a next-word prediction, you train the model with model questions and answers (think of it as mock question paper).
5. Chain of Thought: In this, you train the model with some answers as to how to reason and think through in steps. This is equivalent to our high school / college exam papers (esp. Math) in which we explain the steps in detail without a gap in logic (or making assumptions).
6. Human Feedback - more so, RLHF (Reinforcement Learning with Human Feedback) - this is the main technique that catapulted chatgpt to its success. This is the method by which we teach the model how to write answers that are more acceptable to humans rather than just long strings of text (or coming up with just any number of not so coherent but grammatical sentences).
7. Policy learning: Making the model come up with many different ways to solve a problem and then pick the policy that's the ideal way to solve.
8. Reward learning: Nudging the models to prefer one way of solving / answering by giving it a "reward".
9. KL-Divergence for policy optimization : This is a statistical technique to figure out the difference between two sets (of policies - so a new policy is as close to a tried and tested policy but still efficient).
10. Distillation : which I already mentioned : Having a large and slow but accurate teacher model which creates data for a small and fast but less accurate student model to learn from and eventually become accurate enough.
11. Quantization: Mucking around with floating point numbers. As all of deep learning is pretty much matrix multiplication (think millions and billions of matrices with dimensions in 1000s).
12. Mixture of Experts: Having one large model be composed of many smaller expert models and the model automatically knows "different internal routes" to take.

And I am still probably missing many many more cool ideas and techniques.

## Wow, that's cool, right?

yes, yes, a 1000 times ... this is super cool!

## Wow, but is this real?

That's the big question. There are a whole bunch of charges.
1. The deepseek company is supposed to have done this with 2k chips but they are known to have 10k chips, or 50k chips (based on some reports).

2. There is a huge question about how it could be done for only $6M. And that it should've been at least in the ~50M range.

3. Even if the final model can be accepted to be 6M, it is still unfair -- as one astute post said, "you cannot calculate the metal value of a Toyota camry to be 4K and then suddenly say that anyone can go against Toyota with $5K". 

This is true -- since the Deepseek itself is built with the aid of Meta's Llama (which cost 10s of millions to train and overall capex/opex is in the billions and counting - thanks brother Zuck!). And also with Alibaba's Qwen.

4. There are claims that the RL technique is not for real. Or the dataset is unknown.

There are many efforts to reproduce this paper - so we will know in a month or two (or few), if these claims hold true.

5. The chip export problem.  (How did chips get there? What other bans should be imposed?)

6. The open-source problem. (Will such large models be open sourced any more?)

7. Unlawful use of data. OpenAI / Microsoft are claiming that Deepseek may have used data from openai's model to train their model. Lest not irony humor you that openai itself is facing lawsuits of illegally using copyrighted data.

But but but .....

The cool thing though is that Deepseek published their research (take that OpenAI and Anthropic and whoever else that do not publish anymore). So this is exactly how research is supposed to be. Anyone should be able to verify the claim on their own.

## What's cooler?

This entire set of models are open-source! Meaning anyone can download them (think 7b or 70b or 600b of numbers) to your own machines (even phones) and run them on your own! So you don't even need the internet once it is all set up. The cat is truly out of the bag.

## What else?

In the recent months, we are seeing more and more claims of how it is possible to now train frontier models and even search engines (albeit limited scope) for less than $10M. These are supposed to be billion dollar problems. Or thought to be.

But now they are not. A small lab (okay, in deepseek's case it is about 200+ folks it seems) - but still small teams have a shot at doing cool work.

Even if not foundational models work, they can use these models to do cool stuff on top of this.

The possibilities are mind-boggling and amazing.

We are living in interesting times.

Hopefully that gave you a quick tour of Deepseek's recent announcement and why it is a big deal.

Welcome your feedback, questions or comments. Pardon any mistakes - let me know, happy to learn.

PS: I will post various links in the comments section below.

## Bibliography / Appendix / References

### Deepseek - Use the ~force~ source!

DeepSeek Github and this has the links to the respective papers

[https://github.com/deepseek-ai](https://github.com/deepseek-ai)

[https://github.com/deepseek-ai/DeepSeek-V3](https://github.com/deepseek-ai/DeepSeek-V3)

[https://github.com/deepseek-ai/DeepSeek-R1](https://github.com/deepseek-ai/DeepSeek-R1)


### Commoditizing the Complement - an old (gold) article by Joel Spolsky from early 2000s

This is an old but GOLD article and theory! I love it. It is called Commoditizing the complement. This is probably the best explanation of why Zuck / Meta would give out everything for FREE!!!

[https://www.joelonsoftware.com/2002/06/12/strategy-letter-v/](https://www.joelonsoftware.com/2002/06/12/strategy-letter-v/)

### Thus Spake Andrej Karpathy

Also add, Karpathy's posts:

[https://x.com/karpathy/status/1884336943321997800?s=48](https://x.com/karpathy/status/1884336943321997800?s=48)

[https://x.com/karpathy/status/1883941452738355376?s=48](https://x.com/karpathy/status/1883941452738355376?s=48)

Actually all of Karpathy's posts are worth reading.

Specific call out to "Deep Dive into LLMs": This video is a MUST WATCH!
Yes, it is 3+ hours - but it is worth it.

[https://www.youtube.com/watch?v=7xTGNNLPyMI](https://www.youtube.com/watch?v=7xTGNNLPyMI)

This is an Intro to LLM talk about a year ago - but also very good:

[https://www.youtube.com/watch?v=zjkBMFhNj_g](https://www.youtube.com/watch?v=zjkBMFhNj_g)

And as said above, all of Karpathy's videos are worth watching.

In addition to Karpathy, this Neural Networks video series by Grant Sanderson of 3blue1brown fame is also worth every second:

[https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)


### Explanatory Tutorials

DeepSeek R1 for everyone:

[https://trite-song-d6a.notion.site/Deepseek-R1-for-Everyone-1860af77bef3806c9db5e5c2a256577d](https://trite-song-d6a.notion.site/Deepseek-R1-for-Everyone-1860af77bef3806c9db5e5c2a256577d)

DeepSeek V3:

[https://lunar-joke-35b.notion.site/Deepseek-v3-101-169ba4b6a3fa8090a7aacaee1a1cefaa](https://lunar-joke-35b.notion.site/Deepseek-v3-101-169ba4b6a3fa8090a7aacaee1a1cefaa)

Illustrated DeepSeek R1 by Jay Allamar (of the Illustrated Transformer fame):

[https://newsletter.languagemodels.co/p/the-illustrated-deepseek-r1](https://newsletter.languagemodels.co/p/the-illustrated-deepseek-r1)

Visual Guide to Reasoning Models by Maarten Grootendorst:

[https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-reasoning-llms](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-reasoning-llms)

Visual Guide to Mixture of Experts (MoE) by Maarten Grootendorst:

[https://substack.com/home/post/p-148217245](https://substack.com/home/post/p-148217245)

Putting RL back in RLHF:

[https://huggingface.co/blog/putting_rl_back_in_rlhf_with_rloo](https://huggingface.co/blog/putting_rl_back_in_rlhf_with_rloo)

DeepSeek R1's recipe to replicate o1 and the future of reasoning LMs by Nathan Lambert:

[https://www.interconnects.ai/p/deepseek-r1-recipe-for-o1](https://www.interconnects.ai/p/deepseek-r1-recipe-for-o1)

Understanding Reasoning LLMs by Sebastian Raschka:

[https://magazine.sebastianraschka.com/p/understanding-reasoning-llms](https://magazine.sebastianraschka.com/p/understanding-reasoning-llms)

Deepseek's GRPO technique:

[https://www.philschmid.de/deepseek-r1](https://www.philschmid.de/deepseek-r1)



### More Tutorials

Epoch.ai's write up of DeepSeek's innovations to Transformer Architecture:

[https://epoch.ai/gradient-updates/how-has-deepseek-improved-the-transformer-architecture]

Multihead Latent Attention:

[https://www.pyspur.dev/blog/multi-head-latent-attention-kv-cache-paper-list]

Reasoning from small models with 8k examples:

[https://hkust-nlp.notion.site/simplerl-reason]

[https://github.com/hkust-nlp/simpleRL-reason]

A big list of posts from across various groups:

[https://buttondown.com/ainews/archive/ainews-bespoke-stratos-sky-t1-the-vicunaalpaca/]

All DeepSeek papers and their main contributions:

[https://martinfowler.com/articles/deepseek-papers.html]

LORA Explanation:

[https://athekunal.medium.com/lora-low-rank-adaptation-paper-in-depth-explanation-417f5fa40668]

S1 : The $6 R1 competitor by Tim Kellogg:

[https://timkellogg.me/blog/2025/02/03/s1]

HN Discussion of the above: [https://news.ycombinator.com/item?id=42946854]

Slightly off-topic: A guide to running your own Local LLMs:

[https://www.dbreunig.com/2025/02/04/a-gentle-intro-to-running-a-local-llm.html]


### Various write-ups / opinion pieces

This is a long write up about a short case for Nvidia. This also walks through various other technical things in detail. Worth the read.

[https://youtubetranscriptoptimizer.com/blog/05_the_short_case_for_nvda](https://youtubetranscriptoptimizer.com/blog/05_the_short_case_for_nvda)

Fantastic write up / explanation by Ben Thompson (Stratechery):

[https://stratechery.com/2025/deepseek-faq/](https://stratechery.com/2025/deepseek-faq/)

Brilliant write-up (as always) by Matt Levine (for Bloomberg):

[https://archive.ph/lHjfO](https://archive.ph/lHjfO)

A theory on how Deepseek worked around the export restrictions:

[https://threadreaderapp.com/thread/1883712727073607859.html](https://threadreaderapp.com/thread/1883712727073607859.html)

MODERN-DAY ORACLES or BULLSHIT MACHINES? How to thrive in a ChatGPT world Developed by Carl T. Bergstrom and Jevin D. West

[https://thebullshitmachines.com/table-of-contents/index.html](https://thebullshitmachines.com/table-of-contents/index.html)


Karen Hao's write up:  

[https://www.linkedin.com/posts/karendhao_much-of-the-coverage-ive-been-reading-on-activity-7289652107576545284-Dlw0/](https://www.linkedin.com/posts/karendhao_much-of-the-coverage-ive-been-reading-on-activity-7289652107576545284-Dlw0/)  

An analysis by Ed Zitron:  

[https://www.wheresyoured.at/deep-impact/](https://www.wheresyoured.at/deep-impact/)  

Write up by VentureBeat:  

[https://venturebeat.com/ai/deepseek-r1s-bold-bet-on-reinforcement-learning-how-it-outpaced-openai-at-3-of-the-cost/](https://venturebeat.com/ai/deepseek-r1s-bold-bet-on-reinforcement-learning-how-it-outpaced-openai-at-3-of-the-cost/)  

Stargate announcement:  

[https://bsky.app/profile/hankgreen.bsky.social/post/3lgrhqjr5v22k](https://bsky.app/profile/hankgreen.bsky.social/post/3lgrhqjr5v22k)  

What happened in the markets and why it took so long to react:  

[https://thezvi.substack.com/p/deepseek-panic-at-the-app-store](https://thezvi.substack.com/p/deepseek-panic-at-the-app-store)  

Mythbusters:  

[https://www.linkedin.com/feed/update/urn:li:activity:7289820777304989697/](https://www.linkedin.com/feed/update/urn:li:activity:7289820777304989697/)  

Camry analogy:  

[https://www.threads.net/@tomgara/post/DFX8jeOOJcM](https://www.threads.net/@tomgara/post/DFX8jeOOJcM)  

500M hardware prediction:  

[https://www.ft.com/content/ee83c24c-9099-42a4-85c9-165e7af35105](https://www.ft.com/content/ee83c24c-9099-42a4-85c9-165e7af35105)  

Singapore PM Lee:  

[https://youtu.be/Khgc0JCQ320?si=wHQow0mXMxpv3d5s](https://youtu.be/Khgc0JCQ320?si=wHQow0mXMxpv3d5s)  

Funny twitter:  

[https://x.com/PabloMartell_/status/1883915087532228684](https://x.com/PabloMartell_/status/1883915087532228684)  

Model performance / cost:  

[https://x.com/raveeshbhalla/status/1883380722645512275](https://x.com/raveeshbhalla/status/1883380722645512275)  

FWIW, a great answer by Deepseek CEO:  

[https://x.com/iScienceLuvr/status/1883254324769538075](https://x.com/iScienceLuvr/status/1883254324769538075)  

Ray Dalio is predicting bubble and eventual collapse - calling this equiv to 98/99:  

[https://www.ft.com/content/eef8dbc9-bd04-4502-bdc2-1092aa4251b2](https://www.ft.com/content/eef8dbc9-bd04-4502-bdc2-1092aa4251b2)  

You can do this with a $6K machine:  

[https://x.com/carrigmat/status/1884244369907278106?s=48](https://x.com/carrigmat/status/1884244369907278106?s=48)  

The bull case for Nvidia!  

[https://www.linkedin.com/posts/aleksagordic_guys-its-so-over-this-is-the-future-of-activity-7289969843766755328-Z3zW/](https://www.linkedin.com/posts/aleksagordic_guys-its-so-over-this-is-the-future-of-activity-7289969843766755328-Z3zW/)  

Distillation probe:  

[https://x.com/straits_times/status/1884512558498943394?s=48](https://x.com/straits_times/status/1884512558498943394?s=48)  

OpenAI vs DeepSeek claims:  

[https://www.linkedin.com/posts/kartik-hosanagar-22272115_openai-has-evidence-that-its-models-helped-activity-7290537668025716736-mf0h/](https://www.linkedin.com/posts/kartik-hosanagar-22272115_openai-has-evidence-that-its-models-helped-activity-7290537668025716736-mf0h/)  

WW3:  

[https://www.moneycontrol.com/news/opinion/with-deepseek-on-the-horizon-world-war-iii-has-begun-12921201.html](https://www.moneycontrol.com/news/opinion/with-deepseek-on-the-horizon-world-war-iii-has-begun-12921201.html)  

MODERN-DAY ORACLES or BULLSHIT MACHINES? How to thrive in a ChatGPT world  
Developed by Carl T. Bergstrom and Jevin D. West  

[https://thebullshitmachines.com/table-of-contents/index.html](https://thebullshitmachines.com/table-of-contents/index.html)  


## DISCLAIMER

I am writing this just for the sake of my friends. I have tried my best to keep it readable, entertaining, maybe a bit humorous, all the while trying to keep it to a level that as many people can understand. This required simplifying (very very absurdly at times) topics and explanations and processes.

I am Krishna Srinivasan. And this is me:
[https://linkedin.com/in/krishna2](https://linkedin.com/in/krishna2)

Here is my Google Scholar page:
[https://scholar.google.com/citations?user=aYn5qFUAAAAJ&hl=en](https://scholar.google.com/citations?user=aYn5qFUAAAAJ&hl=en)



