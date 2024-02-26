| Chapter     | Status             |
| ----------- | ------------------ |
| Chapter 1.1 | :white_check_mark: |
| Chapter 1.2 | :white_check_mark: |
| Chapter 1.3 | :white_check_mark: |
| Chapter 1.4 | :white_check_mark: |
| Chapter 1.5 | :white_check_mark: |
| Chapter 2.1 | :white_check_mark: |
| Chapter 2.2 | :white_check_mark: |
| Chapter 2.3 | :white_check_mark: |
| Chapter 2.4 | :warning:          |
| Chapter 3.1 | :white_check_mark: |
| Chapter 3.2 | :warning:          |
| Chapter 3.3 | :warning:          |
| Chapter 3.4 | :white_check_mark: |

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

| **Aspect**           | **Laws of thought    **                                           | **Rational Agent (Ideal for AI)**                                             |
| -------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Definition           | Emphasizes correct inferences as the hallmark of intelligence.    | Focuses on agents that act to achieve the best outcome.                       |
| Objective            | Making correct inferences based on logical rules.                 | Acting to achieve the best outcome or expected outcome.                       |
| Scope                | Primarily concerned with logical reasoning processes.             | Encompasses autonomous operation, perception, adaptation, etc.                |
| Inference            | Central to rational behavior, deducing actions based on premises. | One mechanism among others for achieving rationality.                         |
| Limitations          | Limited applicability in scenarios involving uncertainty.         | More adaptable to real-world scenarios and uncertain environments.            |
| Development Approach | Built on logical foundations, focusing on definite plans.         | Evolves from logical foundations to probabilistic and learning-based methods. |
| Scientific Rigor     | Relies on logical rules and deductive reasoning.                  | Mathematically well-defined, allowing for scientific development.             |

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

Table that might help - GPT made this tho

| **Foundation**    | **Mathematics**                                       | **Logic**                                        | **Algorithms**                                                     | Data                                            | Knowledge                                       | Perception                                                  | Learning                                             | Interaction                                              |
| ----------------- | ----------------------------------------------------- | ------------------------------------------------ | ------------------------------------------------------------------ | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------------------- | ---------------------------------------------------- | -------------------------------------------------------- |
| Description       | Provides theoretical framework for AI.                | Basis for reasoning and problem-solving.         | Computational procedures for problem-solving.                      | Raw information used by AI systems.             | Domain-specific information and expertise.      | Interpretation and understanding of sensory inputs.         | Improvement of performance through experience.       | Communication and collaboration between AI and humans.   |
| Key Concepts      | Calculus, linear algebra, probability theory.         | Deductive, inductive, abductive reasoning.       | Search, sorting, optimization algorithms.                          | Structured, unstructured, semi-structured data. | Facts, rules, concepts, beliefs.                | Vision, speech, text processing.                            | Supervised, unsupervised, reinforcement learning.    | Natural language processing, human-computer interaction. |
| Role in AI        | Provides tools for modeling and analysis.             | Enables logical reasoning and decision-making.   | Implements AI techniques and methodologies.                        | Acts as input for training and decision-making. | Guides reasoning and decision-making processes. | Enables understanding and interaction with the environment. | Facilitates adaptation and optimization of behavior. | Enables effective communication and collaboration.       |
| Examples          | Matrix operations, probability distributions.         | Propositional, predicate logic.                  | Search algorithms (DFS, BFS), sorting algorithms (Quicksort).      | Images, text documents, sensor data.            | Domain-specific rules, concepts, ontologies.    | Image recognition, speech recognition.                      | Personalized recommendations, predictive modeling.   | Chatbots, virtual assistants, recommender systems.       |
| Challenges        | Complexity, scalability, accuracy.                    | Handling uncertainty, incompleteness.            | Efficiency, scalability, optimization.                             | Volume, variety, veracity, velocity.            | Acquiring, representing, updating knowledge.    | Ambiguity, variability, noise.                              | Overfitting, bias, scalability.                      | Natural language understanding, context awareness.       |
| Advancements      | Advanced mathematical techniques (deep learning).     | Automated reasoning (automated theorem proving). | Improved algorithms (machine learning, deep learning).             | Big data technologies (Hadoop, Spark).          | Knowledge graphs, semantic web.                 | Computer vision (object detection, image segmentation).     | Reinforcement learning, transfer learning.           | Conversational AI, affective computing.                  |
| Future Directions | Integration of mathematics with other domains (AI+X). | Automated reasoning in uncertain environments.   | Optimization of algorithms for distributed and parallel computing. | Data quality and reliability assurance.         | Semantic AI, explainable AI.                    | Multimodal perception, embodied AI.                         | Lifelong learning, explainable AI.                   | Human-centric AI, empathetic AI.                         |

## 1.3: History of AI

| **Period**                                                    | **Description**                                                                                                                |
| --------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Inception of AI 1943 - 1956                               | **Birth of AI:** Coined by John McCarthy in 1956 at the Dartmouth Conference.                                                  |
|                                                           | **Key Milestones:** Warren McCulloch and Walter Pitts' neural network model (1943), Alan Turing's Turing Test proposal (1950). |
| Early enthusiasm, great expectations 1952 - 1969          | **Growth Phase:** Rapid progress fueled by optimism and funding.                                                               |
|                                                           | **Notable Achievements**: IBM's Logic Theorist (1956), John McCarthy's Lisp programming language (1958).                       |
|                                                           | **Challenges:** Limited computing power and memory, leading to simplistic models.                                              |
| Dose of reality 1966 - 1973                               | **AI Winter Begins:** Funding cuts, unmet expectations, and skepticism.                                                        |
|                                                           | **Notable Events**: DART project failure (1966), Criticism from the Lighthill Report (1973).                                   |
|                                                           | **Shift in Focus**: Emphasis on rule-based systems and knowledge representation.                                               |
| Expert systems 1969 - 1986                                | **Rule-Based AI**: Focus on developing expert systems for specific domains.                                                    |
|                                                           | **Notable Systems**: MYCIN (diagnostic system), DENDRAL (chemical analysis).                                                   |
|                                                           | **Limitations**: Difficulty in encoding knowledge, lack of adaptability.                                                       |
| Return of neural networks 1986 - present                  | **Neural Network Resurgence**: Rediscovery of backpropagation and advances in computing power.                                 |
|                                                           | **Notable Milestones**: Backpropagation breakthrough (1986), Convolutional Neural Networks (CNNs) for image recognition.       |
|                                                           | **Applications**: Speech recognition, image classification, natural language processing.                                       |
| Probabilistic Reasoning & Machine Learning 1987 - present | **Statistical AI**: Integration of probabilistic reasoning and machine learning techniques.                                    |
|                                                           | **Notable Developments**: Hidden Markov Models (HMMs), Support Vector Machines (SVMs), Reinforcement Learning.                 |
|                                                           | **Applications**: Predictive modeling, pattern recognition, data mining.                                                       |
| Big data 2001 - present                                   | **Data Revolution**: Emergence of massive datasets and tools for storage and analysis.                                         |
|                                                           | **Impact on AI**: Enables training of more complex models and deep learning architectures.                                     |
|                                                           | **Challenges**: Data quality, privacy concerns, scalability issues.                                                            |
| Deep learning 2011 - present                              | **Deep Learning Dominance**: Breakthroughs in deep neural networks and architectures.                                          |
|                                                           | **Notable Achievements**: AlexNet's victory in ImageNet competition (2012), AlphaGo's defeat of Go world champion (2016).      |
|                                                           | **Applications**: Autonomous vehicles, healthcare diagnostics, natural language understanding.                                 |

## 1.4: State of the art

| Topic                            | State of the Art                                                                                                   |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Robotic Vehicles                 | - Advanced autonomous driving systems like Tesla Autopilot and Waymo's self-driving technology.                    |
|                                  | - Integration of AI for real-time decision-making, perception, and navigation in vehicles.                         |
| Legged Locomotion                | - Advancements in quadruped and bipedal robots like Boston Dynamics' Spot and Atlas robots.                        |
|                                  | - Use of AI for dynamic balance, obstacle negotiation, and terrain adaptation in legged robots.                    |
| Autonomous Planning & Scheduling | - AI-powered systems for resource allocation, task scheduling, and logistics optimization.                         |
|                                  | - Integration of machine learning for adaptive planning and real-time adjustments in schedules.                    |
| Machine Translation              | - State-of-the-art neural machine translation models like Google Translate and DeepL.                              |
|                                  | - Use of transformer-based architectures and large-scale training data for improved translation quality.           |
| Speech Recognition               | - Highly accurate speech recognition systems like Google's Speech-to-Text and Amazon Transcribe.                   |
|                                  | - Integration of deep learning models for robust performance in various languages and accents.                     |
| Recommendations                  | - Personalized recommendation systems in platforms like Netflix, Amazon, and Spotify.                              |
|                                  | - Utilization of collaborative filtering, content-based filtering, and deep learning for accurate recommendations. |
| Game Playing                     | - AI agents capable of superhuman performance in games like Chess, Go, and Dota 2.                                 |
|                                  | - Development of reinforcement learning algorithms and deep neural networks for game strategy.                     |
| Image Understanding              | - State-of-the-art image classification, object detection, and segmentation models.                                |
|                                  | - Use of convolutional neural networks (CNNs) and transfer learning for robust image understanding.                |
| Medicine                         | - AI applications in medical diagnosis, drug discovery, and personalized treatment planning.                       |
|                                  | - Integration of deep learning, natural language processing, and computer vision in medical research.              |
| Climate Science                  | - AI-based models for climate prediction, extreme weather detection, and climate change analysis.                  |
|                                  | - Utilization of machine learning for data analysis, pattern recognition, and climate modeling.                    |

## 1.5: Risks & Benefits of AI

| Topic                        | Risks                                                      | Benefits                                                              |
| ---------------------------- | ---------------------------------------------------------- | --------------------------------------------------------------------- |
| Lethal Autonomous Weapons    | - Potential for misuse leading to indiscriminate harm.     | - Reduced risk to human soldiers in combat situations.                |
|                              | - Lack of accountability and ethical oversight.            | - Enhanced precision and efficiency in military operations.           |
| Surveillance and Persuasion  | - Invasion of privacy and erosion of civil liberties.      | - Improved public safety and crime prevention.                        |
|                              | - Manipulation of public opinion and behavior.             | - Enhanced monitoring and response to security threats.               |
| Biased Decision Making       | - Reinforcement of existing biases and discrimination.     | - Increased efficiency and automation in decision-making.             |
|                              | - Unfair treatment and perpetuation of inequality.         | - Potential for unbiased and data-driven decision-making.             |
| Impact on Employment         | - Job displacement and economic inequality.                | - Increased productivity and economic growth.                         |
|                              | - Loss of traditional livelihoods and skills.              | - Creation of new job opportunities and industries.                   |
| Safety-Critical Applications | - Potential for catastrophic failures and accidents.       | - Enhanced reliability and efficiency in critical systems.            |
|                              | - Limited ability to predict and mitigate risks.           | - Improved performance and safety in transportation, healthcare, etc. |
| Cybersecurity                | - Vulnerabilities exploited for malicious purposes.        | - Improved defense against cyber threats and attacks.                 |
|                              | - Potential for widespread disruption and damage.          | - Development of secure systems and protocols.                        |
| AI Superintelligence         | - Existential risks from uncontrolled super intelligent AI. | - Accelerated scientific and technological progress.                  |
|                              | - Loss of human control over AI systems.                   | - Potential solutions to complex global challenges.                   |

## Summary
- Different goals drive AI approaches: focus on thinking or behavior, modeling humans or optimizing results.
- The standard model of AI prioritizes rational action, aiming to build intelligent agents.
- Challenges arise due to computational limitations and the need for machines to pursue human-beneficial objectives.
- Philosophy: Suggested mind-machine similarity, knowledge encoding, and thought-action link.
- Mathematics: Provided tools for logical and probabilistic reasoning, computation understanding.
- Economics: Formalized decision-making to maximize expected utility.
- Neuroscience: Uncovered brain-computer similarities and differences.
- Psychology: Considered humans and animals as information processors, with language fitting into this model.
- Computer Engineering: Enabled AI applications through powerful hardware and usable software.
- Control Theory: Designed devices for optimal action based on environmental feedback, increasingly intersecting with AI.
- History: Marked by cycles of success, optimism, funding cutbacks, and innovative approaches.
- Methodological evolution: Transitioned from Boolean logic to probabilistic reasoning and from hand-crafted knowledge to machine learning.
- Real-world applications: Raised concerns about risks and ethical implications.
- Long-term challenges: Addressing control and unpredictability of super intelligent AI systems, prompting reevaluation of AI conception.

---

# Chapter 2
## 2.1: Agents & Environments
- Agent
	- An agent is an entity that acts on its environment via actuators based on precept data from its sensors in the environment
		- A precept sequence is the history of everything that the agent has perceived
		- An Agent Function specifies the action taken by the agent in response to any precept sequence
		- f = p<sup>*</sup> -> A
			- f = Agent function
			- p<sup>*</sup> = Perceived info
			- A = Action performed
		- Agent = Architecture + Program, where architecture is the hardware and program is the precept sequence
## 2.2: Good behavior: Rationality concept
- What makes for a rational Agent
	- Performance Measures
		- Actions taken by an agent that lead it closer to the goal state via a desirable path
	- Rationality
		- The performance measure that defines the criterion of success.
		- The agent’s prior knowledge of the environment.
		- The actions that the agent can perform.
		- The agent’s percept sequence to date.
	- Omniscience, Learning & Autonomy
		- If an agent acts on the design it was created for and not the precepts then it lacks autonomy
		- An agent must be able to assimilate as much information as possible from its precepts
		- Omniscience i.e. knowing what the result of every outcome will be is impossible for a computer but it it doable based on precept history and predictions
## 2.3: Nature of Environments
- Specifying Task Environments
	- For a rational agent we need a way to classify its attributes which are
		- Performance Measure: The goals to keep in mind
		- Environment: the scope of the agent which is expected to pull in data from and operate in
		- Actuators: Action mechanisms available to the agent
		- Sensors: Data available via selected inputs to the agent
- Properties of Task environments

| Property       | Description                                                                                                                                                                                                                     |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Observability  | **Fully Observable:** The agent can directly and completely observe the entire state of the environment. <br> **Partially Observable:** The agent's view of the environment is limited; it cannot observe all aspects directly. |
| Agent Type     | **Single Agent:** There is only one agent operating in the environment. <br> **Multiagent:** Multiple agents are present, each with its own goals and actions.                                                                  |
| Determinism    | **Deterministic:** Given a particular state and action, the outcome is certain and predictable. <br> **Nondeterministic (Stochastic):** Actions may lead to different outcomes with certain probabilities.                      |
| Temporality    | **Episodic:** Each action sequence is independent of previous ones; the agent's experience is divided into episodes. <br> **Sequential:** Actions are interdependent, and the current action may affect future ones.            |
| Dynamics       | **Static:** The environment does not change while the agent is deliberating. <br> **Dynamic:** The environment can change while the agent is deciding on its actions.                                                           |
| Discretization | **Discrete:** The state and/or action space are finite and countable. <br> **Continuous:** The state and/or action space are infinite and uncountable.                                                                          |
| Knowledge      | **Known:** The agent has complete knowledge of the environment's dynamics and rules. <br> **Unknown:** The agent lacks complete information about the environment, such as its dynamics or rules.                               |

Some examples from the book

| Task              | Observability        | Agent Type   | Determinism      | Temporality | Dynamics | Discretization | Knowledge |
| ----------------- | -------------------- | ------------ | ---------------- | ----------- | -------- | -------------- | --------- |
| Crossword Puzzle  | Partially Observable | Single Agent | Deterministic    | Episodic    | Static   | Discrete       | Known     |
| Chess             | Fully Observable     | Multiagent   | Deterministic    | Sequential  | Dynamic  | Discrete       | Known     |
| Poker             | Partially Observable | Multiagent   | Nondeterministic | Sequential  | Dynamic  | Discrete       | Known     |
| Taxi Driving      | Partially Observable | Single Agent | Nondeterministic | Sequential  | Dynamic  | Continuous     | Known     |
| Medical Diagnosis | Partially Observable | Single Agent | Nondeterministic | Sequential  | Dynamic  | Discrete       | Known     |
| Image Analysis    | Fully Observable     | Single Agent | Deterministic    | Sequential  | Static   | Continuous     | Known     |
| Teaching          | Partially Observable | Single Agent | Nondeterministic | Sequential  | Dynamic  | Discrete       | Known     |

## 2.4: Structure of Agents
- **Simple reflex agents:**
	    - They select actions solely based on the current percept, without considering past percepts or future consequences.
	    - These agents operate using a set of condition-action rules.
	    - Infinite loops can occur in partially observable environments, where crucial information might be missing.
		    - Can break of these loops however if the agent randomly picks its actions
	- **Pseudocode:**
		- Function: Simple-Reflex-Agent
			- persistent: rules, set of condition-action rules
			- state <- interpret-input(precept)
			- rule <- Rule-match(state, rules)
			- action <- rule.Action()
			- return action
- **Model-based reflex agents:**
	- To handle partial observability, keep track of the part of the enviro it cannot see right now
- **Goal-based agents:**
	- Also referred to as problem-solving agents, they seek sequences of actions that lead to desirable states or goals.
	- These agents utilize problem-solving algorithms, like depth-first search or A* search, to find optimal or satisficing solutions.
	- Goal-based agents involve a goal formulation stage, where the agent determines what needs to be achieved, followed by a search for a solution to reach that goal.
- **Utility-based agents:**
	- These agents make decisions by evaluating the utility or desirability of different outcomes.
	- They consider not only whether a state achieves a goal but also how desirable that outcome is, as quantified by a utility function.
	- Utility-based agents can handle situations where there are multiple conflicting goals by prioritizing actions based on their expected utility.
- Learning agents
- How the components of agent programs work


---

# Chapter 3
## 3.1: Problem Solving Agents
- Search problems & solutions
	- A search problem has
		- State space: a set of possible states the environment can be in
		- Initial State: starting state of the agent
		- Goal State: ending state of the agent, can be multiple
		- Actions: Possible actions the agent can perform to alter their environment
			- Path: Sequence of actions
			- Solution: Path from initial to goal state
			- Optimal Solution: Solution with lowest path cost
		- Transition Model: defines what an action will do. like what a function will return essentially
		- Action Cost: Gives numeric cost of applying action A in state S to reach state S'
	- Assuming that the agent always has information about the environment we can adopt a 4-Phase problem solving process
		- Goal Formulation: Adopt a goal state
		- Problem Formulation: Decide what actions/states to consider given a goal
		- Search: Simulate a sequence of possible actions in its model
		- Execution: Execute the actions one at a time
- Formulating Problems
	- Concept of abstraction is applied here.
## 3.2: Example Problems
- Standardized problems
	-
- Real-world problems
## 3.3: Search Algorithms
-  %% Best-First Search %%
- Search Data structures
- Redundant paths
- Measuring problem-solving performance
## 3.4: Uninformed Search Strategies
- Breadth-first search
	- Start with the initial node.
	- Enqueue it into the queue.
	- Dequeue a node from the queue and expand it.
	- Enqueue all of its unvisited neighbors.
	- Repeat until the goal node is found or the queue is empty.

```pseduocode
BFS(graph, start_node, goal_node):
    initialize an empty queue
    enqueue the start_node onto the queue
    while queue is not empty:
        current_node = dequeue from the queue
        if current_node is goal_node:
            return path to goal
        for each neighbor of current_node:
            if neighbor has not been visited:
                mark neighbor as visited
                enqueue neighbor onto the queue
    return "goal not found"

```

- Uniform-Cost search (Dijkstra's algo)
	- Start with the initial node with cost 0.
	- Enqueue it into the priority queue.
	- Dequeue a node from the priority queue with the lowest cost.
	- Update the cost to its neighbors if a lower cost path is found.
	- Repeat until the goal node is found or the priority queue is empty.

```pseduocode
Dijkstra(graph, start_node):
    initialize an empty priority queue
    enqueue start_node with priority 0
    while priority queue is not empty:
        current_node = dequeue from the priority queue
        if current_node is goal_node:
            return path to goal
        for each neighbor of current_node:
            new_cost = cost_to_current_node + cost_of_edge
            if new_cost < cost_to_neighbor:
                update cost_to_neighbor
                enqueue neighbor with priority new_cost
    return "goal not found"
```

- Depth-First search
	- Start with the initial node.
	- Push it onto the stack.
	- Pop a node from the stack and expand it.
	- Push all of its unvisited neighbors onto the stack.
	- Repeat until the goal node is found or the stack is empty.

```pseduocode
DFS(graph, start_node, goal_node):
    initialize an empty stack
    push the start_node onto the stack
    while stack is not empty:
        current_node = pop from the stack
        if current_node is goal_node:
            return path to goal
        for each neighbor of current_node:
            if neighbor has not been visited:
                mark neighbor as visited
                push neighbor onto the stack
    return "goal not found"
```

- Depth-Limited
	- For Depth-Limited Search (DLS), set a maximum depth limit and perform DFS up to that limit.

```pseduocode
DLS(graph, start_node, goal_node, depth_limit):
    recursive_DLS(start_node, goal_node, depth_limit)
    
recursive_DLS(current_node, goal_node, depth_limit):
    if current_node is goal_node:
        return path to goal
    if depth_limit is 0:
        return "cutoff"
    for each neighbor of current_node:
        if neighbor has not been visited:
            mark neighbor as visited
            result = recursive_DLS(neighbor, goal_node, depth_limit - 1)
            if result is not "cutoff" and result is not "goal not found":
                return result
    return "cutoff"
```

- Iterative Deepening Search
	- For Iterative Deepening Search (IDS), repeatedly perform DLS with increasing depth limits until the goal is found.

```pseduocode
IDS(graph, start_node, goal_node):
    for depth_limit from 0 to infinity:
        result = DLS(graph, start_node, goal_node, depth_limit)
        if result is not "cutoff" and result is not "goal not found":
            return result
```

- Bidirectional Search
	- Start BFS from both the start and goal nodes simultaneously.
	- Meet in the middle when both searches intersect.
	- Combine paths from both searches to form the solution path.
	- PseudoCode

```pseducode
BidirectionalSearch(graph, start_node, goal_node):
    initialize an empty forward_queue and backward_queue
    enqueue start_node into forward_queue
    enqueue goal_node into backward_queue
    while both forward_queue and backward_queue are not empty:
        forward_node = dequeue from forward_queue
        backward_node = dequeue from backward_queue
        if forward_node is in backward_queue:
            return path from start_node to forward_node + path from goal_node to forward_node
        for each neighbor of forward_node:
            if neighbor has not been visited:
                mark neighbor as visited
                enqueue neighbor into forward_queue
        for each neighbor of backward_node:
            if neighbor has not been visited:
                mark neighbor as visited
                enqueue neighbor into backward_queue
    return "goal not found"
```

- Comparing Uninformed Search Algorithms

| Criterion     | BFS              | UCS                                              | DFS              | DLS              | IDS              | BiS                |
| ------------- | ---------------- | ------------------------------------------------ | ---------------- | ---------------- | ---------------- | ------------------ |
| Complete?     | Yes<sup>1</sup>  | Yes<sup>1,2</sup>                                | No               | No               | Yes<sup>1</sup>  | Yes<sup>1,4</sup>  |
| Optimal Cost? | Yes<sup>3</sup>  | Yes                                              | No               | No               | Yes<sup>3</sup>  | Yes<sup>3,4</sup>  |
| Time          | O(b<sup>d</sup>) | O(b<sup>1 + [<sup>C\*<sup/>/<sub>e</sub>]</sup>) | O(b<sup>m</sup>) | O(b<sup>l</sup>) | O(b<sup>d</sup>) | O(b<sup>d/2</sup>) |
| Space         | O(b<sup>d</sup>) | O(b<sup>1 + [<sup>C\*<sup/>/<sub>e</sub>]</sup>) | O(b\m)           | O(b\*l)          | O(b\*d)          | O(b<sup>d/2</sup>) |

- Key
	- b = Branching factor
	- m = Maximum Depth
	- d = Depth of shallowest solution, M if there is no solution
	- L = depth limit
- Caveats
	- 1: Complete if b is finite
	- 2: Complete if all action costs are >= e > 0
	- 3: Cost-Optimal if all action costs are all identical
	- 4: If both directions are Breadth-First or Uniform Cost