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
- Philosophy
	- Examines fundamental questions about knowledge, truth, and existence.
	- Influences AI ethics and decision-making.
	- Provides the basis for understanding logic and reasoning in AI systems.
	- Questions
		- Can formal rules be used to draw valid conclusions?
		- How does the mind arise from the physical brain
		- Where does knowledge come from
		- How does knowledge lead to action
- Mathematics
	- Provides formal logic and reasoning tools.
	- Utilizes mathematical models for analysis and optimization of AI algorithms.
	- Applies mathematical concepts for AI algorithm development and optimization.
	- Questions
		- What are the formal rules to draw valid conclusions
		- What can be computed
		- How do we reason with uncertain information
	- Turing showed that no machine in general can tell that a given program will return an answer on a given input or run forever
	- Intractable problems; time required to solve instances of a given problem grows exponentially
	- NP-Completeness;
- Economics
	- Analyzes decision-making processes, incentives, and resource allocation.
	- Utilizes economic models to understand economic systems and behaviors.
	- Integrates economic principles into AI system design and optimization.
- Neuroscience
	- Explores brain structure, function, and neural networks.
	- Applies neuroscience findings to study brain function and cognition.
	- Utilizes knowledge of brain processing for AI modeling and optimization.
- Psychology
	- Studies human behavior, cognition, and perception.
	- Examines human decision-making and cognition.
	- Provides insights into human behavior and cognition to inform AI design.
- Computer Engineering
	- Shapes hardware and software design for AI systems.
	- Informs AI system design based on human behavior and cognition.
	- Utilizes neural networks and feedback mechanisms for AI modeling and optimization.
- Control Theory & Cybernetics
	- Investigates feedback systems and control mechanisms.
	- Applies principles of feedback and control for AI systems.
	- Utilizes feedback mechanisms to optimize AI performance and self-regulation.
- Linguistics
	- Explores language structure, syntax, semantics, and pragmatics.
	- Utilizes knowledge of linguistic structures for NLP algorithms.
	- Applies principles of feedback and control for language acquisition and processing in AI systems.



Table that might help

| Foundation        | Mathematics                                           | Logic                                            | Algorithms                                                         | Data                                            | Knowledge                                       | Perception                                                  | Learning                                             | Interaction                                              |
| ----------------- | ----------------------------------------------------- | ------------------------------------------------ | ------------------------------------------------------------------ | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------------------- | ---------------------------------------------------- | -------------------------------------------------------- |
| Description       | Provides theoretical framework for AI.                | Basis for reasoning and problem-solving.         | Computational procedures for problem-solving.                      | Raw information used by AI systems.             | Domain-specific information and expertise.      | Interpretation and understanding of sensory inputs.         | Improvement of performance through experience.       | Communication and collaboration between AI and humans.   |
| Key Concepts      | Calculus, linear algebra, probability theory.         | Deductive, inductive, abductive reasoning.       | Search, sorting, optimization algorithms.                          | Structured, unstructured, semi-structured data. | Facts, rules, concepts, beliefs.                | Vision, speech, text processing.                            | Supervised, unsupervised, reinforcement learning.    | Natural language processing, human-computer interaction. |
| Role in AI        | Provides tools for modeling and analysis.             | Enables logical reasoning and decision-making.   | Implements AI techniques and methodologies.                        | Acts as input for training and decision-making. | Guides reasoning and decision-making processes. | Enables understanding and interaction with the environment. | Facilitates adaptation and optimization of behavior. | Enables effective communication and collaboration.       |
| Examples          | Matrix operations, probability distributions.         | Propositional, predicate logic.                  | Search algorithms (DFS, BFS), sorting algorithms (Quicksort).      | Images, text documents, sensor data.            | Domain-specific rules, concepts, ontologies.    | Image recognition, speech recognition.                      | Personalized recommendations, predictive modeling.   | Chatbots, virtual assistants, recommender systems.       |
| Challenges        | Complexity, scalability, accuracy.                    | Handling uncertainty, incompleteness.            | Efficiency, scalability, optimization.                             | Volume, variety, veracity, velocity.            | Acquiring, representing, updating knowledge.    | Ambiguity, variability, noise.                              | Overfitting, bias, scalability.                      | Natural language understanding, context awareness.       |
| Advancements      | Advanced mathematical techniques (deep learning).     | Automated reasoning (automated theorem proving). | Improved algorithms (machine learning, deep learning).             | Big data technologies (Hadoop, Spark).          | Knowledge graphs, semantic web.                 | Computer vision (object detection, image segmentation).     | Reinforcement learning, transfer learning.           | Conversational AI, affective computing.                  |
| Future Directions | Integration of mathematics with other domains (AI+X). | Automated reasoning in uncertain environments.   | Optimization of algorithms for distributed and parallel computing. | Data quality and reliability assurance.         | Semantic AI, explainable AI.                    | Multimodal perception, embodied AI.                         | Lifelong learning, explainable AI.                   | Human-centric AI, empathetic AI.                         |



## 1.3: History of AI
Inception of AI 1943 - 1956
Early enthusiasm, great expectations 1952 - 1969
Dose of reality 1966 - 1973
Expert systems 1969 - 1986
Return of neural networks 1986 - present
Probabilistic Reasoning & Machine Learning 1987 - present
Big data 2001 - present
Deep learning 2011 - present

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