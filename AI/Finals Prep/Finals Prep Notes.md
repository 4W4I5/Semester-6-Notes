| Chapter                                             | Status        |
| --------------------------------------------------- | ------------- |
| Chapter 2.1: Agents & Enviros                       | :exclamation: |
| Chapter 2.2: Concept of Rationality                 | :exclamation: |
| Chapter 2.3: Nature of Enviros                      | :exclamation: |
| Chapter 2.4: Agent Structure                        | :exclamation: |
| Chapter 3.1: Problem Solving Agents                 | :exclamation: |
| Chapter 3.2: Examples                               | :exclamation: |
| Chapter 3.3: Search Algos                           | :exclamation: |
| Chapter 3.4: Uninformed Searches                    | :exclamation: |
| Chapter 3.5: Informed Heuristic Searches            | :exclamation: |
| Chapter 3.6: Heuristic Functions                    | :exclamation: |
| Chapter 4.1: Local Search & Optimization Problems   | :exclamation: |
| Chapter 4.2: Local Search in Continuous Spaces      | :exclamation: |
| Chapter 4.3: Search with Nondeterministic Actions   | :exclamation: |
| Chapter 4.4: Search in Partially Observable Enviros | :exclamation: |
| Chapter 4.5: Online Search Agents & Unknown Enviros | :exclamation: |
| Chapter 5.1: Game Theory                            | :exclamation: |
| Chapter 5.2: Optimal Decisions in Game              | :exclamation: |
| Chapter 5.3: Heuristic AB Search + Pruning          | :exclamation: |
| Chapter 5.7: Limitations of Game Search Algos       | :exclamation: |
| Chapter 6.1: Defining CSP                           | :exclamation: |
| Chapter 6.2: Inference in CSP                       | :exclamation: |
| Chapter 6.3: Backtracking Search for CSP            | :exclamation: |
| Chapter 6.4: Local Search for CSP                   | :exclamation: |
| Chapter 6.5: Struct of Problems                     | :exclamation: |
| Machine Learning Slides 31                          | :exclamation: |
| Machine Learning Slides 32                          | :exclamation: |
| Machine Learning Slides 33                          | :exclamation: |
| Machine Learning Slides 34                          | :exclamation: |
| Machine Learning Slides 35                          | :exclamation: |
| Machine Learning Slides 36                          | :exclamation: |
| Machine Learning Slides 37                          | :exclamation: |
| Machine Learning Slides 38                          | :exclamation: |

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
		- Can be human, robotic or just software
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
	- To handle partial observability, keep track of the part of the enviro it cannot see right now i.e. maintain a state of what its seen so far
		- Knowledge of how the world changes over time needed i.e. a transition model
			- Effects of the agents actions
			- How the world evolves independent of the agent
		- State of the world reflected in the agent's precepts i.e. a sensor model
	- Both models are used to keep a track on the state of the world
	- **Pseudocode:**
		- Function: Model-Based-Agent
			- persistent: state, current conception of the world state, transition + sensor model, rules, action
			- state <- Update-State(state, action, precept, transition-model, sensor-model)
			- rule <- Rule-match(state, rules)
			- action <- rule.Action()
			- return action
- **Goal-based agents:**
	- Also referred to as problem-solving agents, they seek sequences of actions that lead to desirable states or goals.
	- Behavior is based off of model agents but now they have a goal to seek out i.e. actions that favor the goal state are chosen
	- Now we test for how the enviro is affected based off of our choice, this allows us to pick the most favorable action
	- Only provides a crude binary however b/w satisfactory state and unsatisfactory state
	- **Pseudocode:**
		- Function: Model-Based-Agent
			- persistent: state, current conception of the world state, transition + sensor model, rules, action
			- state <- Update-State(state, action, precept, transition-model, sensor-model)
			- testState <- Update-State(state, action, precept, transition-model, sensor-model)
			- if testState more favorable than state then
				- rule <- Rule-match(testState, rules)
			- else
				- rule <- Rule-match(state, rules)
			- action <- rule.Action()
			- return action
- **Utility-based agents:**
	- These agents make decisions by evaluating the utility or desirability of different outcomes.
		- Maximizes expected utility i.e. the probability that the action chosen grants high utility
	- They consider not only whether a state achieves a goal but also how desirable that outcome is, as quantified by a utility function.
	- Utility-based agents can handle situations where there are multiple conflicting goals by prioritizing actions based on their expected utility.
	- Add to Pseudocode
		- Compare action with utility meter and observe which one is the highest, return that action
- Learning agents
	- Any agent can be a learning agent
	- Just a problem generator to it
	- Concept division of 4
		- Critic
			- Compares data from precept and performance standards to provide feedback
		- Learning element
			- Uses feedback from critic to bias the performance element fed by precepts
			- Provides learning goals to the problem generator
		- Performance element
			- Provides knowledge back to the learning element as well as performing the actions based off of data from the learning element, precepts and problem generator
		- Problem generator
			- Uses learning goals to create new problems i.e. new precept sequences are suggested. Kind of like the randomized reflex agent in a partially observable world
- How the components of agent programs work
	- Atomic Representation:
		- Represents knowledge as indivisible units or atomic propositions.
		- Each proposition represents a single fact.
		- Simplifies reasoning by breaking problems into smaller pieces.
		- May struggle with capturing complex relationships.
	- Factored Representation:
		- Breaks knowledge into smaller components or attributes.
		- Variables represent different states or conditions.
		- Allows for more flexibility and expressiveness.
		- Considers interactions and dependencies between variables.
		- Managing many variables can become complex.
	- Structured Representation:
		- Organizes knowledge using hierarchical or relational structures.
		- Groups related information into graphs, trees, or frames.
		- Captures rich semantic relationships and dependencies.
		- Efficient retrieval and manipulation of knowledge.
		- Design and maintenance may require significant effort.

---

# Chapter 3 (Shorten)
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
- **Standardized Problems**:
	- **Vacuum Robot**: Tasked with efficiently cleaning a space, requiring path planning and obstacle avoidance.
	- **Sokoban**: Puzzle game involving moving boxes in a maze, needing route-finding algorithms like A* search.
- **Real-world Problems**:
	- **Travelling Salesman Problem (TSP)**: Seeks the shortest route visiting locations once, vital in logistics and transportation.
	- **Tourist Route Planning**: Involves optimizing travel itineraries for tourists, blending TSP and route optimization techniques.
## 3.3: Search Algorithms (skipped cause meh)
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