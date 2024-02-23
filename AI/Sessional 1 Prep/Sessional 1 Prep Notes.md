| Chapter     | Status |
| ----------- | ------ |
| Chapter 1.1 | :white_check_mark:    |
| Chapter 1.2 | :x:    |
| Chapter 1.3 | :x:    |
| Chapter 1.4 | :x:    |
| Chapter 1.5 | :x:    |
| Chapter 2.1 | :x:    |
| Chapter 2.2 | :x:    |
| Chapter 2.3 | :x:    |
| Chapter 2.4 | :x:    |
| Chapter 3.1 | :x:    |
| Chapter 3.2 | :x:    |
| Chapter 3.3 | :x:    |
| Chapter 3.4 | :x:    |

<!--
:white_check_mark:
:x:
-->


# Chapter 1
## 1.1: What is AI
- Turning Test
	- A computer that has the following attributes will **participate** in the test
		- Natural Language Processing, to communicate successfully
		- Knowledge Representation, to store what it knows/hears
		- Automated Reasoning, to answer questions and draw new conclusions
		- Machine Learning, to adapt new circumstances and to detect + extrapolate patterns
		- Optional
			- The total Turing test requires CV, Speech recognition and Robotics in order to better fool the test observer
	- Test Details
		- Observer is placed in a room
		- One human and One AI are placed in another room as players, both can communicate with the observer. The observer cannot see either of them.
		- Observer and Players take turns communicating with each other or completing assigned tasks. The AI and Human player take turns answering the observer
		- The concept is that the AI must be able to fool the observer into thinking that it was the human player all along
	- Issues with the test
		- Imitation of life is not the goal of AI. The goal is to understand how intelligence in organisms works in order to use that concept in AI
- Cognitive Modelling | The way humans think
	- Theory of the mind
		- **Introspection**, catch our own thoughts as they go by
		- **Psychological Experiments**, observing a person in action
		- **Brain imaging**, observing the brain in action
	- Can express the theory as a computer program once these 3 domains are understood
- Beneficial Machines
	- The standard model of AI assumes that a fully specified objective will be provided to the machine, but this may not be suitable in the long run.
		- In tasks like chess or shortest-path computation, the objective is inherent, making the standard model applicable. However, in real-world scenarios like designing a self-driving car, specifying the objective becomes increasingly challenging.
	- Value alignment problem:
		- Arises when the objectives programmed into the machine must align with human values, particularly problematic in human-robot interaction scenarios.
			- In lab or simulated environments, incorrect objectives can be easily corrected
			- In real world deployments, this approach becomes untenable due to potential negative consequences.
	- The standard model's inadequacy is evident when considering the potential misbehavior of intelligent machines pursuing fixed objectives, highlighting the need for a new formulation.
	- Machines should pursue human objectives rather than their own, necessitating a formulation where machines are uncertain about the complete objective and incentivized to act cautiously and defer to human control.
	- Ultimately, the goal is to develop agents that are provably beneficial to humans, addressing the value alignment problem.
- Laws of thought vs Rational Agent

| Aspect               | Laws of thought                                                   | Rational Agent (Ideal for AI)                                                               |
| -------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Definition           | Emphasizes correct inferences as the hallmark of intelligence.    | Focuses on agents that act to achieve the best outcome.                       |
| Objective            | Making correct inferences based on logical rules.                 | Acting to achieve the best outcome or expected outcome.                       |
| Scope                | Primarily concerned with logical reasoning processes.             | Encompasses autonomous operation, perception, adaptation, etc.                |
| Inference            | Central to rational behavior, deducing actions based on premises. | One mechanism among others for achieving rationality.                         |
| Limitations          | Limited applicability in scenarios involving uncertainty.         | More adaptable to real-world scenarios and uncertain environments.            |
| Development Approach | Built on logical foundations, focusing on definite plans.         | Evolves from logical foundations to probabilistic and learning-based methods. |
| Scientific Rigor     | Relies on logical rules and deductive reasoning.                  | Mathematically well-defined, allowing for scientific development.                                                                              |

## 1.2: Foundations of AI
## 1.3: History of AI
## 1.4: State of the art
## 1.5: Risks & Benefits of AI
---

# Chapter 2
## 2.1: Agents & Environments
## 2.2: Good behavior: Rationality concept
## 2.3: Nature of Environments
## 2.4: Structure of Agents
---

# Chapter 3
## 3.1: Problem Solving Agents
## 3.2: Example Problems
## 3.3: Search Algorithms
## 3.4: Uninformed Search Strategies