# Chapter 1: Random Variables and Probabilities

### A motivating example
* Need a broad motivating problem: you own a spaceship, and have been asked to go on a mission. Your engine isn’t working. What do you do? 
* Form a hypothesis about why the engine isn’t working: maybe you suspect that a small alien rodent has gnawed through your fuel lines? 
* The fuel lines are unfortunately hidden behind a radiation shield: getting at them is a huge pain which you’d rather avoid if you could. 
* Thus, you want to collect observations that would give you meaningful information
* You’ve seen droppings around, so you definitely know there’s a rodent. You just don’t know whether it’s wreaked havoc
* So you design an experiment: there’s a pressure gauge on the fuel lines. If you increase the flow of fuel, the pressure rises linearly. However, if there is a leak, then fuel is lost, and the pressure will not go above a certain value, because another fuel is just lost through the leak
You go ahead and slowly increase the flow of fuel, and tell your trusty assistant to measure the pressure. Unfortunately, there’s also an issue with the pressure gauge (your space ship really is quite old, but pressure gauges were an expense fairly far down the list), and so it jitters around as your assistant is desperately trying to read off the values. 
* In the end, they hand you a list of values, and you look at it. 
[MAYBE GENERATE SOME DATA HERE AND A PLOT]
So how do we figure out what’s going on?  —> student exercise?


## Introduction

In scientific research, our core goal is to gain knowledge about the world we live in, 
be that knowledge about stars, about how rocks form, or about how a certain drug affects 
out bodies. We look for relationships between phenomena we observe, and we look for patterns 
and (physical) laws that could describe those phenomena. We design experiments and make 
observations that can help us discover new relationships, or test the proposed laws we have 
written down for those we have already found. However, our experiments and observations are 
never perfect. All too often, we have to *infer* that knowledge using incomplete information: 
we cannot (yet) fly to a star and probe it directly (except, maybe, our own sun), and similarly, 
we can never test a drug on _all_ possible patients. This limitation injects _uncertainty_ into 
our conclusions; the field of statistics develops methods and toolds for dealing rigorously 
with that uncertainty. 
Often, statistics is taught with a "cook-book" approach of recipes that you can apply to data to 
derive certain numbers, without an accompanying explanation of how one arrives at that particular 
recipe, why it works and what happens if you forget the (metaphorical) butter. If you are anything 
like us, the authors, this can lead to a lot of uncertainty and apprehension. When we first learned 
statistics, we did not know why a certain type of statistical method worked, or worse, why it provided 
a number we didn't expect. We also often didn't know which test to use, or why to use a certain test 
but not another. In this course, we aim to give you both: useful background knowledge for the 
mathematical principles that underly much of the statistics we use in research, where it comes from, 
how to use it in practice, and what to do if it goes wrong (and how to find out whether it has 
gone wrong in the first place). 


## Scientific Inference and Box' Loop

In scientific research, we often start with a i*hypothesis* or theory: an explanation for a phenomenon, 
often described in terms of relations or equations. Often, we are looking for _causal_ relationships: 
whether for example a supermassive black hole is the cause for the drop-off in star formation in its 
host galaxy, or, closer to home, whether a specific drug has a causal effect on someone's health. 
However, hypotheses need not be causal: we can also construct a hypothesis that suggests a connection 
between two phenomena, without specifying causality. Often, looking for *correlations* can be a good 
first step when we do not know enough about a phenomenon or system to come up with possible causal 
relationship. 

It is worth mentioning here, then, that correlation and causation are not the same thing, and you 
must take care not to confuse the two (if you do, do not worry, you are in good company!).  
For example, there might be a correlation between the amount of ice cream consumed on a given day 
and the rate of sunburns on that same day, but there is no causal link between the two: eating ice 
cream does not cause sunburn, nor does a sunburn cause an increase in ice cream consumption. Instead, 
both are caused by a different, underlying phenomenon we might not have thought of and consequently 
not measured: whether it is sunny or not!

A hypothesis is most useful for scientific research--independent of whether it posits a causal 
relationship between quantities or not--if it makes *predictions* about those quantities, especially 
if we can design an experiment or observations of those quantities. The scientific process 
crucially rests on the ability to make predictions, and then test them against observations of the 
real world to figure out whether the hypothesis is compatible with Nature.  
This process is called *inference*, i.e.~a comparison between the predictions and observations enabling 
us to learn whether our hypothesis reasonably describes the underlying phenomenon. If our observations 
indeed match closely the predictions, we consider that evidence in support of the hypothesis, and 
similarly observations that are substantially different we use as evidence against the hypothesis.

This is all fairly abstract: we have not yet talked about what it actually means, in practice, to 
compare observations to hypothesis (hint: it's more than squinting at them and going 'yeah, all right'). 
Similarly, we'll need some more formal definition of what it means for observations to "closely match" 
our observations. Giving you those formal definitions, methods and tools is what most of this course 
is concerned with.

It is helpful here to mention that astronomy is an _observational_ science. With few examples, we cannot 
carry out experiments: we cannot easily change the mass of a star and see how it reacts, or throw a 
test mass into a black hole. For the most part, we are restricted to passively observing the universe, 
and interpreting what we see. This is in contrast to experimental physics, for example, or microbiology.
But we are in good company of other fields, including parts of epidemiology, climate science, geology and 
others. In astronomy, science is often an _iterative_ process, in part because of the fairly large 
role of serendipity in astronomy. All too often, new phenomena are discovered by chance, and we then need 
to start developing hypotheses about these chance discoveries we can then test with new observations. 
For example, Gamma-Ray Bursts were first discovered in the 1970s purely by chance in observations of 
satellites meant to monitor nuclear testing in the Earth's atmosphere. It took until the mid 1990s before 
even the question of whether they originated in our galaxy or outside of it were settled, and it took even 
longer before there was solid evidence for their cause in stellar explosions. 
Along the way, researchers constructed both causal hypotheses ("Some Gamma-Ray Bursts are caused by the explosion 
of very massive stars") and non-causal hypotheses ("There are two distinct classes of GRBs with different 
physical origins"), they designed new observing campaigns (and even entire telescopes and instruments, such 
as the Fermi Gamma-Ray Burst Monitor) to gather new data, and then revised hypotheses when data and 
hypothesis disagreed. 

This is an example of *Box' Loop* of iterative inference (REF BLEI). 
If we do not know where else to start, we start with what is called *Exploratory Data Analysis*, where 
we might search broadly for relationships in the data. Based on these initial explorations, we might start 
building simple hypotheses about the origin of the phenomenon we have observed. We then collect new data, 
and use an inference algorithm (we will get to those!) to test the model or hypothesis against our data. 
A crucial step is then to identify the ways in which our model succeeds, and which it fails to reproduce 
the data. If we are not satisfied with the model's performance, or the hypothesis is in contrast to the 
data we have gathered, it is time to go back to the drawing board and revise the model according to the 
results of our *model criticism* (which we will talk about in the latter part of the course). With our 
revised model, we can then collect new data and repeat the cycle. 


### Deductive Versus Inductive Reasoning  

Two types of reasoning: deductive and inductive
* Deductive reasoning follows the rules of logic to arrive at a conclusion, given a premise
* Conclusions are true as long as the premises are true
* Mathematics based on deductive reasoning
* Conclusions are inescapable given premises —> this is why we can write down proofs in mathematics
* Deduction involves reasoning from the general to the specific
* Also applies to probabilistic and deterministic theories —> will talk about this more when we talk about the rules of probability
Inductive reasoning: from specific to general
* Describe arguments from special cases to general ones, or from effects to causes
* Given that the sun has risen every day for many days, we can inductively reason that it will rise tomorrow, but we don’t ultimately know: there is no logical conclusion that this must happen
* Does not have the same power as deductive reasoning
* Conclusions arrived at by inductive reasoning is not necessarily due, it is based on incomplete information —> statistics helps us quantify how much we believe it to be true

### Uncertainty

Our information about the real world is almost always incomplete, affected by random uncertainty, or both
For example, to predict the outcome of an election, researchers ask a subset of the population about how they will vote, because asking everyone is infeasible. However, this leaves us with incomplete information: We’ve not asked everyone, just a small fraction of people who will vote. From there, we try to infer how the population as a whole will vote. But not everyone in that group may actually vote on the day of the election (even if they say they are planning to), and not everyone will give a truthful answer to the interviewer (they might not want the interviewer to know their political leanings, or they might simply change their mind). All of these introduce uncertainty into our prediction of an election outcome
sample: a subset of a population used to infer something about the population as a whole
Small samples easy to collect, but more susceptible to random fluctuations. If a certain party usually receives 5% of the seats in parliament, and in my survey I have only asked 10 people for their opinion, there is no way I can get a good estimate for how many people will vote for that party. If one or more people say they’ll vote for that party, my estimate will be 10% or more. If nobody says they’ll vote for that party, my estimate is 0%. Either of them are off by a large margin. This type of variation is also called random error (by physicists) or uncertainty
Need to sample randomly and in an unbiased fashion: for example, traditionally people tend to become more conservative with age, so surveying people at a university might lead to different predictions for the election outcome than, say, surveying people in a retirement community.    
Similar problems arise in astrophysics: for example, because apparent brightness is a function of the square of the distance, we preferentially see the brightest galaxies with increasing distance (and thus age). If we don’t account for that effect in our analyses, we might conclude that galaxies used to be much brighter than they are today. This is usually called systematic error or bias. 

question: how to reason in situations where it is not possible to argue with certainty

Student exercise: What is probability?
Have students explore some examples and definitions, maybe crowdsource 

Starts with James Bernoulli (1713) who looked at the difference between deductive logic applied to games of chance versus inductive reasoning applied to everyday life
Bayes and Laplace: considered probability a degree-of-belief or plausibility: how much do we think something is true, based on the evidence at hand?
Seemed to vague and subjective to 19th century scholars as a basis for a rigorous mathematical theory
Alternative definition: probability as a long-run relative frequency with which an event occurred, given (infinitely) many repeated (experimental) trials
Frequencies can be measured, probability considered an objective tool to deal with random phenomena
In some ways more limited: often, in science, we actually want to quantify our degree of uncertainty about something that is *not* random (e.g. the mass of a black hole) 
In the frequentist perspective, we have to imagine an ensemble of universes in which everything remains constant apart from the mass of that black hole, or at least be able to repeat the experiment many times 
Frequentist statistics can be very powerful when we indeed consider random phenomena, but can be a bit more complicated when looking at problems where we are interested in quantifying our uncertainty about the world
Here, we will consider both: one approach is not more correct than they other, and different communities prefer different approaches (and have different standards)
Bayesian inference (where we consider probability as degree-of-belief) can often be very computationally expensive, and for many problems, we would arrive at the same conclusion as we would with a (conceptually more complex, but computationally much simpler) formulation of a frequentist problem 


Types of uncertainty
Two reasons for uncertainty in our predictions for a certain outcome
Ignorance of the underlying  hidden causes or mechanism generating our data: called epistemic uncertainty (epistemology is the philosophical term to describe the study of knowledge)
* Simpler term: model uncertainty
Second uncertainty arises from intrinsic variability, and cannot be reduced by collecting more data
Sometimes called aleatoric uncertainty (from the latin word for “dice”) or data uncertainty

### Probability
Define an “event”, denoted by the binary variable A, as some state of the world that either does or does not hold (e.g. “it will rain tomorrow”, “it rained yesterday”, …)
* Could be, for example, a single outcome of an experiment, or a set of outcomes 
$A$ is also called a *random variable*. The set of possible values this variable could take (here, two, since we have defined it to be binary for now) is called the *sample space* or *state space*. An *event* is a set of outcomes from a given sample space. 
Pr(A) is the probability with which you believe that event A is true (or the long-run fraction of times that A will occur)
Cox studied the quantitative rules necessarily for logical and consistent reasoning
Want to express our relative beliefs in the truths of statements, such as A 
For multiple statements A and B and C, we also want to be able to rank them in a transitive manner (so that if A is more probable than B, and B is more probable than C, then A should also be more probable than C)
We can do that by assigning real numbers to A and B and C
Cox specified that if we have defined how much we believe something to be true, we have also implicitly specified how much we believe that it is false, because those are the only two possible outcomes
Using Boolean logic, Cox worked out how to formalise these ideas —> become the basic rules of probability
Probabilities lie between 0 and 1, such that $0 \leq \mathrm{Pr}(A) \leq 1$, where $\mathrm{Pr}(A) = 0$ denotes certainty that the event did not happen, and $\mathrm{Pr}(A) = 1$ indicates that the event $A$ definitely did happen
The complement of A, often written $A^C$ or $\bar{A}$, is the belief that A is false. Because $A$ must either happen or *not* happen, the sum of $A$ and its complement $\bar{A}$ must be $1$, since we have decided that this denotes certainty: $ Pr(A) + Pr(\bar{A}) = 1$. 
In the same vein, we can write $Pr(\bar{A}) = 1 - Pr(A)$
Of course, one can imagine that one might have multiple possible outcomes. For example, let’s say the weather has four (mutually exclusive) states: $W_1 = \mathrm{“sunny”}$, $W_2 = \mathrm{“cloudy”}$, $W_3 = \mathrm{“rainy”}$, $W_4 = \mathrm{“snowy”}$ (remember how we initially said that we’re building simplified models of the world? This is one of them!). Since the weather has to be *one* of those, we can write $\sum_{i=1}^{4} Pr(W_i) = 1$. 
It is helpful to use some notation from set theory: 
$A \cup B$ can be read as “A or B” or the union of A and B. In Boolean logic, a statement will be true if either of A or B are true. 
$A \cap B$ can be read as “A and B”, or the intersection of A and B. Here, a statement is only true if both A *and* B are true
We can extend this to probabilities. For example, $Pr(A \cup \bar{A}) = 1$, because either A or its complement must be true. 
Conversely, $Pr(A \cap \bar{A}) = 0$, because A and its complement cannot, by definition, both be true at the same time. 
Now let’s imagine we have two events, $A$ and $B$ [ADD EXAMPLE].

What about either $A$ *or*$ $B$ happening? Well, that depends on whether $A$ and $B$ are mutually exclusive, that is, whether there is a chance that they could occur together or not.
If two events $A$ and $B$ are mutually exclusive, then the probability of observing either $A$ *or$ $B$ is simply the sum of the individual probabilities: $Pr(A \cup B) = Pr(A) + Pr(B)
If they are not mutually exclusive, then we need to include a correction term to account for the fact that $Pr(A)$ implicitly also includes $Pr(A, B)$ and similarly $Pr(B)$ also includes $Pr(A, B)$. Thus, we have counted a part of the probability space twice, and need to correct for that double-counting:
$Pr(A \cup B) = Pr(A) + Pr(B) - Pr(A, B)$. 

### Conditional Probability + Bayes Rule

Above, we have discussed the probability of either $A$ or $B$ happening. But what about the probability of both happening together?
Pr(A \cap B) = Pr(A, B) is called the *joint probability* of A and B, describing the probability that both A and B will occur at the same time. 
EXAMPLE FOR $Pr(A, B)$
Obviously, for mutually exclusive events as described above, $Pr(A \cup B) = 0$. 
If the occurrence of A does not affect the occurrence of be (or vice versa), then A and B are said to be *statistically independent*. In mathematical terms, we can write $Pr(A, B) = Pr(A) Pr(B)$. This means, for both events $A$ and $B$ to occur simultaneously, we must multiply the probabilities for each occurring individually together. This makes some intuitive sense: The probability of both $A$ and $B$ occurring together should be smaller than the probability of either one of those individual events happening. 

More interesting, however, is the case where $A$ and $B$ are _not* statistically independent. This is called a _conditional probability_, or $Pr(A | B)$, where the vertical bar “|” is pronounced as “given”, such that the whole expression indicates the probability of $A$ given $B$. It assumes that $B$ has already happened with a probability of $Pr(B) = 1$, and we would now like to know what the probability is that $A$ will _also_ happen. Intuitively, you might still say that we should simply multiply both probabilities together, but this is not so! Instead, we need to account for the fact that $B$ has already happened, which “shrinks” our probability space [Probably need a Venn diagram of some sort here?]. 
So the probability of observing $A$, given that $B$ has already happened, is 
$ Pr(A | B)  = \frac{Pr(A, B)}{Pr(B)}$. 
Similarly, we can also calculate the probability of $B$ happening, if $A$ has already happened: $Pr(B | A) = \frac{Pr(A, B)}{Pr(A)}$. 
Note, and this is important, that the probability of $A$ occurring given $B$ is not the same as the probability of $B$ occurring given that $A$ has already happened, unless $A$ and $B$ are statistically independent. You can see this with a simple example: What’s the probability that it’s raining ($R$) given that it’s cloudy ($C$)? Conversely, what’s the probability that it’s cloudy, given that it’s raining? It should be immediately obvious that $Pr(R | C)$ is probably going to be significantly smaller than $Pr(C | R)$: living in The Netherlands, we get extraordinarily many cloudy days, even when it’s not raining. However, when it’s raining, you can be pretty sure that there are clouds (the rain has to come from somewhere, doesn’t it?). Conditional probability is a really fundamental concept in statistics that we will come back over and over (and that appears in many other applications beyond this class). 

* Can you think of other situations where $Pr(A | B) \neq Pr(B |A)$? Share some examples!

[NEED AN EXERCISE HERE]

You might have noticed that there is a common term in the definitions for $Pr(A | B)$ and $Pr(B | A)$: both contain the joint probability, $Pr(A, B)$. This means we can actually directly relate the two conditional probabilities together, without having to calculate the joint probability (this will turn out to be extremely useful in practice later): 

$Pr(A | B) = \frac{Pr(B | A)Pr(A)}{Pr(B)}$
 This equation is called Bayes’ Rule, after Reverend Bayes who first discovered it (it was later rediscovered by Laplace in 1812 and used with great effectiveness to solve real-world problems, including a fairly precise estimation of the mass of Saturn using orbital data. In modern data analysis, it is the basis of what is now called “Bayesian Statistics”, which rests upon the interpretation of probability as a degree-of-belief, and is being used across the sciences to infer knowledge about our world. 


—— 

Exercise/plot Idea 


You’re in the station’s shop trying to get outfitted for your first mission. 
You don’t have any money for the shiny gadgets on the wall. “How about a lucky draw?”, the shopkeeper suggests, gesturing towards a box where he collects assorted gadgets to be picked randomly for a fixed price. 
—> use this to set up probability? 
—> more examples of things in the shop 
Maybe there’s a sketchy character in the shop, too, who already drew something out of the bin, and you have to calculate the probability that they might use that gadget to rob you once you step out?




