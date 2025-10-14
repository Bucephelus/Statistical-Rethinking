#bayesian #statsbook  
[[Statistical Rethinking]]

- All statistical modelling has two frames: *the small world* of the model itself and the *large world* we hope to deploy the model in.
- What is the small world? The self-contained logical world of the model, with the small all world, all possibilities are nominated.
- What is the large world? The broader context in which one deploys a model. In the large world, there may indeed be events that were not imagined in the small world. The logical consistency of a model in the small world is no guarantee that it will be optimal in the large world. 
- Bayesian models learn from evidence (optimal in the small world). 

### 2.1 The garden of forking data
- In order to make good inference about what actually happened, it helps to consider everything that could have happened. 
- She might kill the man, or rather take a cup of tea.
- A Bayesian analysis is a garden of forking data, in which alternative sequences of events are cultivated. As we learn about what did happen, some of these alternative sequences are *pruned*. 

#### 2.1.1 Counting possibilities
- He counts the number of ways a particular observed sequence of marble draws could have occurred *given* and assumed true state of the bag (a hypothesis, which he calls a *conjecture*).
- He wants to determine which state of the world is most likely given the evidence. 
- Numbers multiplied during calculation doesn't change the fact that it is still just a counting of logically possible paths. 
#### 2.1.2 Combining other information 
- We may have additional information about the *relative plausibility* of each conjecture. 
- We have a bag with 4 marbles in it, each one being white or blue. Based on a sample from the bag, we want to infer what make up of all marbles is. Our unknown parameter is $p$, the proportion of marbles that are blue (or white). $p$ can be one of 5 choices: $p \in (0, 0.25, 0.5, 0.75, 1)$. We are selecting randomly with replacement: 
	- If we take $N=3$ draws and $X=2$ is the number that were blue, then we can say that 
			$X \sim \text{Binomial}(N=3, p)$
	- This matches the book because there is a finite number of marbles, and we are re-scaling to be in absolute terms relative to that, instead of rate terms. 
- A *prior* distribution: we may know something about how the bag was arranged, such that we have an idea that a particular value of $p$ is more likely to be true than the rest. 
- Wouldn't your *priors* technically always reflect the most recent information, up to the very second? If we set an initial prior, and then collected a single sample, and updated our model, shouldn't the posterior of that model now be our prior for any subsequent estimate? These are equivalent ways to think about the mathematical procedure, since you are just enumerating the ways that your sequence of observation could have been *observed*. 
- There is no circumstance where we should claim we know *absolutely nothing* about. Even if it is just a little, include it in the model. 

### 2.2 Building a model 
- Suppose we have a globe representing the Earth. It is small enough to hold in your hands, and you are curious how much of the surface is covered in water. Thus, you adopt the following test: you toss the globe up in the air. Once you catch it, you will record whether or not the surface under your right index finger is water or land. You keep doing this and it generates a sequence of samples from the globe, the first nine samples are: 
						W L W W W L W L W
- We observe 6 W and 3 L observations. We call these observations the *data*. 
- To get the logic running, we have to make assumptions and these assumptions constitute the model. Our simple Bayesian model benefits from the following design loop: 
	1) Data story: motivate the model by narrating how the data might arise
	2) Update: educate the model by feeding it the data
	3) Evaluate: all statistical models require supervision, leading to revision of our model. 

#### 2.2.1 A data story
- We have to produce a story for how the data came to be. It may be *descriptive*, specifying associations that can be used to predict outcomes, given our observations. It may be *causal*, a theory of how some events may produce other events. 
- He says that all data stories are complete, in the sense that they are sufficient for specifying an algorithm for simulating new data. We simply restate the sampling process:
	1) The true proportion of water covering the globe is $p$. 
	2) A single toss of the globe has a probability $p$ of producing a water (W) observation. 
	3) Each toss of the globe is independent of the others. 
- The probability model is easy to build, because the construction process can be broken down into a series of component decision. 

#### 2.2.2 Bayesian updating 
- A Bayesian model begins with one set of plausibilities assigned to each of these possibilities. These are the prior plausibilities. Then it updates them in light of the data, in order to produce the posterior plausibilities. This updating process is called Bayesian updating (learning).
- Let's initially assign the same plausibility to every proportion of water, every value of $p$. After we see the first toss, which is a W, the model updates the plausibilities to the solid line. The plausibility of $p=0$ has now fallen to exactly 0 - the equivalent of *impossible*. This is because we saw observed at least one speck of water on the globe, so now we know there is *some* water. 