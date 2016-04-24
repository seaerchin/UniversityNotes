# Artificial Intelligence Part I

## Intelligent Agents
### What is an agent?
- An **agent** is an entity that
- A **rational agent** is one that does the right thing.
		- Actions
		- Goals/Performance Measure
		- Environment (States)
- An **autonomous agent** does not rely entirely on built-in knowledge about the environment. It adapts to the environment through experience & *learning*.
- An **agent program** is a function that implements the agent mapping from percepts to actions.

### Types of Agents
#### Simple Reflex Agent
1. Find the rule whose condition matches the current situation (as defined by the percept).

#### Reflex Agents with State (Model-Based)

**Note:** The *state* is a description of the current world state. It contains all the necessary information to predict the effects of an action and to determine if the state is a goal state.

#### Goal-Based Agents
1. Find the action that will get me closer from my current state to the goal state.
2. Perform that action.

**Note:** A *goal* can be specific (explicit destination), abstract (speed, safety) or numerous.

#### Utility-Based Agents
- There may be many action sequences that can achieve the same goal.
- Which action sequence should the agent take?
	- The one with the maximum utility i.e. lowest cost.

### Types of Environment
- **Accessible (vs Inaccessible)**

## Problem Formulation
### Problem-Solving Agent
- Rational Goal-Based Agent

#### Steps
	- No Knowledge → Random Search
	- Knowledge → Directed Search

### Types of Problems
1. **Single-State Problem**
	- accessible world state (sensory information is available)
	- known outcome of action (deterministic)
	- inaccessible world state (with limited sensory information) i.e. agent only knows which sets of states it is in
	- known outcome of action (deterministic)
3. **Contingency Problem**
	- limited or no sensory information (inaccessible)
	- limited agent knowledge, action result is not predictable
	- effect of action depends on what is found to be true through perception/monitoring (non-deterministic)
	- problem solving requires sensing during the execution phase
4. **Exploration Problem**
	- no information is known about the world state and outcome of action
	- experimentation is often needed
		- Hypotheses as actions, search in the real world
		- Learning builds the agent's knowledge of states and actions progressively

### Well-Defined Formulation
- Definition of a Problem
	- State Space i.e. states reachable from the initial state
	- Goal Test Predicate
	- Cost Function
- Solution
- Search Cost
	- Does the agent find a solution?
	- Is it a good solution? (i.e. with a low path cost)
	- What does it cost to find the solution?
- Total Cost of Problem-Solving
	- Search Cost + Path Cost
	- Trade-offs often required
		- Search for a very long time for an optimal solution
		- Search for a shorter time for a *good enough* solution.

## Search
- A **search algorithm** explores the state space by generating successors of already-explored states i.e. expanding the states.
- A **search strategy** is defined by picking the order of node expansion. Performance of strategies are evaluated by the following metrics:
	- **Completeness:** Does it always find a solution if one exists?
	- **Time Complexity:** How long does it take to find a solution?
	- **Space Complexity:** How much memory is needed to perform the search?
	- **Optimality:** Does it always find the best (least-cost) solution?

### Performance Evaluation
- Measuring difficulty in AI problem:
	- Branching Factor (max. number of successors of any node)
	- Depth of Shallowest Goal Node
	- Maximum Length of Any Path in State Space
- Time Complexity
	- measured in terms of the number of nodes generated during search
- Space Complexity
	- measured in terms of the maximum number of nodes stored in memory
- Search Cost
	- depends on time complexity
	- can also include memory usage
- Total Cost
	- combines the search cost and solution cost (path cost of solution found)

### Search Strategies
- Uninformed Search Strategies
		- Uniform-cost Search
		- Depth-first Search
		- Depth-limited Search
		- Iterative Deepening Search
	- usually more efficient

## Uninformed Search
### Variables
- *b*: Max. Branching Factor
- *d*: Depth of Least-Cost Solution
- *m*: Max. Depth of State Space

### Breadth-First Search
- Expand shallowest unexpanded node, which can be implemented using a FIFO queue.
- Complete: Yes
- Optimal: Yes, when all steps cost equally
- Time: *1 + b + b<sup>2</sup> + b<sup>3</sup> + ... + b<sup>d</sup> = O(b<sup>d</sup>)*
- Space: Assuming every node is kept in memory, *O(b<sup>d</sup>)*.

### Uniform-Cost Search
- To consider edge costs, expand unexpanded node with the least path cost *g*.
	- Modification of BFS.
	- Instead of FIFO queue, using a priority queue with path cost *g(n)* to order the elements.
	- BFS = UCS with *g(n)* = *Depth(n)*
- Complete: Yes
- Optimal: Yes

### Depth-First Search
- Expand deepest unexpanded node, which can be implemented using a LIFO stack. Backtrack only when no more expansion is possible.
- Complete:
	- Infinite-depth Spaces: No
	- Finite-depth Spaces w/ Loops: No
	- Finite-depth Spaces w/o Loops: Yes
- Time: *O(b<sup>m</sup>)*
- Space: *O(bm)*
- Optimal: No

### Depth-Limited Search
- To avoid infinite searching, DFS with a cutoff on the max. depth *l* of a path.
- Complete: Yes, if *l* &ge; *d*
- Time: *O(b<sup>l</sup>)*
- Space: *O(bl)*
- Optimal: No

### Iterative Deepening Search
- Improvement on DLS. Iteratively estimate the max. depth *l* of DLS one-by-one.
- Complete: Yes
- Time: *O(b<sup>d</sup>)*
- Space: *O(bd)*
- Optimal: Yes

## Informed Search
- Uninformed search strategies have a systematic generation of new states but are inefficient.
- Informed search strategies use problem-specific knowledge to determine which node to expand next.

#### Best First Search
- Expand most desirable unexpanded node.
	- Use an evaluation function *f(n)* to estimate the cost of each node.
	- Nodes are ordered so that the one with the lowest *f(n)* is expanded first.
	- The choice of *f* determines the search strategy.

#### Heuristic Function
- Cost function as performance measure.
	- Path Cost Function *g(n)*
		- Cost from initial state to current state (search-node) *n*.
		- No information on the cost towards the goal.
	- Need to estimate cost to the closest goal.
- **Heuristic Function*****h(n)*****:**
	- Estimated cost of the cheapest path from the state at node *n* to a goal state.
		- Exact cost cannot be determined.
	- Depends only on the state at that node.
	- Additional knowledge of the problem is imparted to the search algorithm.
	- Non-negative, problem specific function.
	- If *n* is a goal node, then *h(n) = 0*.

### Greedy Best-First Search
- Expands the node that appears to be closest to goal.
- The cost is estimated using problem-specific knowledge.
- Useful but potentially fallible.
- Complete: No
- Time: *O(b<sup>m</sup>)* (Worst Case)
- Space: *O(b<sup>m</sup>)* (Worst Case)
- Optimal: No
- With a good heuristic function, the complexity can be reduced substantially.
- Uniform-Cost Search:
	- *g(n)*: Path cost to reach node *n* from the start node (Past
	- Optimal & Complete, but inefficient.
- Greedy Best-First Search:
	- *h(n)*: estimated cost of the cheapest path from node *n* to goal node (Future Cost).
	- Neither optimal nor complete but relatively more efficient.
- Combining, UCS & GBFS:
	- *f(n) = g(n) + h(n)*
	- *f(n)*: Estimated total cost of the cheapest path through node *n* from start node to goal.
	- Complete & Optimal when *h(n)* satisfies certain conditions.

#### Optimality of A* Search
- If *h* is admissible, then the tree-search version of A* search is optimal.

#### Complexity of A*
- Time: exponential in length of solution
- Space: exponential in length of solution
- With a good heuristic, significant savings are still possible compared to uninformed search methods.
- Variants of A* search exist to deal with complexity issues.

### Heuristics
#### Admissible Heuristic
- *h\*(n)*: True cost from node *n* to goal.
- A heuristic is admissible if ***h(n) &le; h\*(n)*** for all *n*.
- An admissible heuristic should never overestimate the cost to reach the goal
- i.e. *f(n)* never overestimates the actual cost of a path through node *n* to the goal.

#### Dominance
- *h<sub>2</sub>* dominates *h<sub>1</sub>* if ***h<sub>2</sub>(n) &ge; h<sub>1</sub>(n)*** for all *n*.
- Domination translates to efficiency.
- Always better to use a heuristic function with higher values as long as it does not overestimate the cost.
- If no heuristic dominates, ***h(n) = max(h<sub>1</sub>(n), h<sub>2</sub>(n), ... , h<sub>m</sub>(n)***.

### Relaxed Problem
- A problem with fewer restrictions on the actions compared to an original problem is called a relaxed problem.
- State space graph of the relaxed problem is a supergraph of the original state space.
- Removal of restrictions creates more edges in the graph.

#### Heuristics from Relaxed Problems
- The cost of an optimal solution to a relaxed problem is an admissible heuristic for the original problem.

## Constraint Satisfaction Problems
- Goal: Discover some state that satisfies a given set of constraints.
- State: Defined by variables *V<sub>i</sub>* with values from domain *D<sub>i</sub>*.
- Goal Test: A set of constraints specifying allowable combinations of values for subsets of variables.
- Constraints can be unary (involving one variable), binary (involving two variables) or high-order (involving more than two variables).

#### Definitions
- A state of the problem is defined by an assignment of values to some or all of the variables.

### CSP Incremental Formulation
- States: defined by the values assigned so far
- Goal Test: all variables assigned, no constraints violated

### Search
- No. of Variables: *n*
- Max. Depth of Space: *n*
- Depth of Solution State: *n* (all variables assigned)
- Search Algorithm: Depth-First Search

#### Backtracking
- Simple DFS wastes time searching when constraints have already been violated.
- Solution: Before generating successors, check if constraints have been violated. If yes, backtrack to last decision point and continue.

#### Heuristics/Methods for CSP
- Plain backtracking is an uninformed algorithm.
- General-Purpose Heuristics:
	- Which variable to assign next?
	- In which order should the possible values be tried for each variable?
- Forward Checking & Constraint Propagation:
	- Implications of current variable assignments on the other unassigned variables.

**Most Constraining Variable / Degree Heuristic**

- The variable to be assigned next should be the variable that is involved in the largest number of constraints on unassigned variables.
- This reduces the branching factor on future choices.
- Useful to optimise the order of variable assignments.

**Most Constrained Variable / Minimum Remaining Values Heuristic**

- The variable to be assigned next should be the variable with the fewest possible values.
- Useful to complement *Most Constraining Variable* in case of a tie.

**Least Constraining Value**

- Choose the value for a variable that leaves the largest choice of values for other constraint-related variables.
- Useful to prevent deadlocks, reduce backtracking.

**Forward Checking**

- When a variable *X* is assigned, look at each unassigned variable *Y* connected to *X* and delete from *Y* any value that is inconsistent with the value chosen for *X*.

**Constraint Propagation**

- *Forward Checking* does not look far enough ahead.
- Constraint propagation involves propagating the implications of a constraint on one variable onto all other variables.

#### Local Search
- **Complete-State Formulation:**
	- States: Every state is a complete assignment that might or might not satisfy the constraints.
	- Goal Test: All variables assigned & no constraints violated.
- **Local Search:**
	- The solution path does not matter.
	- The next state is a *neighbour* of the current state.
- **Minimum Conflicts Heuristic:**
	- Choose a value for a variable that results in the fewest conflicts with other variables.

## Adversarial Search for Game Playing
### Properties of a Game
- Deterministic.
- Action of two agents alternate.
- Utility values at the end of the game are always equal and opposite (i.e. adversarial).

### Game as a Search Problem
- Initial State: The board position and the player to move is identified.

### Minimax Algorithm
#### MIN & MAX
- Assumption: You are **MAX**.
- In a normal search problem, the optimal solution is a sequence of moves leading to a goal state - a terminal state that is a win.
- In a game, MIN affects the solution.
- The optimal strategy cannot perform worse than any strategy against an infallible opponent (i.e. MIN plays optimally) - it maximises the worst case outcome for MAX.

#### Minimax Algorithm
- Minimax algorithm performs a depth-first exploration of the game tree.
- Time: *O(b<sup>m</sup>)*, *b* is the no. of legal moves at each point and *m* is the max. depth of the tree.
- Space: *O(bm)* if it generates all the successors at once, or *O(m)* if it generates successors one at a time.
- For real games, the time cost is impractical.

### &alpha;-&beta; Pruning
- In minimax search, the number of game states to examine is exponential in the number of moves.

**General Idea**

- If *m* is better than *n* for Player, then
	- the state with utility *n* will never be reached
	- and hence can be pruned away

#### &alpha;-&beta; Pruning
- &alpha; is the lower bound of optimal utility.
- &beta; is the upper bound of optimal utility.
- The maximiser is always trying to push the value of &alpha; up.
- The minimiser is always trying to push the value of &beta; down.
- If the node's value is between &alpha; & &beta;, then the players might reach it.
- At the beginning (root of the tree), we set &beta; to &infin; and &alpha; to -&infin;.

#### Advantages
- Pruning does not affect the final result.
- Effectiveness depends on the order in which successor nodes are examined.
- In the ideal case, the time complexity can be reduced to *O(b<sup>m/2</sup>)*.

### Games with Elements of Chance
- Non-deterministic games have random elements that can affect the operators.
- This increases the size of the search space.
- The assumption that the opponent minimises utility does not hold.
	- Chance nodes need to be added to the MAX & MIN nodes.
	- Probability needs to be taken into account.