# Simulation

This simulation models how knowledge propagates and becomes synchronized in a peer-to-peer network through dynamic epistemic updates. The simulation is executed by calling the function:

epistemic_simulation(num_agents, num_ticks, p_connection)

where:

- num_agents is the number of P2P agents (nodes) in the network,
- num_ticks is the total number of simulation ticks (time steps), and
- p_connection is the probability that any two agents are directly connected.

## Overview

Initially, each agent is completely uncertain about the state of three propositions:

- contract
- a_contract
- b_contract
This uncertainty is captured by assuming that each agent considers all eight unique possible worlds as possible. (These worlds represent every combination of truth values for the three propositions.) A fixed domain of eight worlds is defined and shared by all agents. Each agent’s epistemic state is represented as a subset of these worlds.

### Random Role Assignment
At the beginning of the simulation, roles are randomly assigned:

- Contract Owner: One agent is randomly selected as the contract owner. This agent is responsible for learning (and later broadcasting) that the contract exists.
- Signer A and Signer B: Two different agents are randomly chosen from the remaining agents to act as the signers. Signer A will later broadcast that a_contract is true, and Signer B will broadcast that b_contract is true.
This random assignment ensures that the simulation is stochastic, so the roles and hence the subsequent flow of information may vary each time the simulation is run.
After we run the function we get a random p2p network with random connection and 3 agents are assigned to 1) learn about the contract, 2) be signer a, 3) be signer b.


## Propagation of Epistemic Updates
### Predefined Epistemic Actions
At specific ticks, certain agents update their epistemic state with a predefined announcement. For example:

- At tick 1 and tick 2, the contract owner updates its epistemic state with {"contract": True} and immediately broadcasts this fact to its direct neighbors.
- At tick 3, Signer A broadcasts that {"a_contract": True}.
- At tick 4, Signer B broadcasts that {"b_contract": True}.
  
When an agent receives a broadcast (whether predefined or dynamically scheduled), it updates its epistemic state by filtering out those worlds that do not satisfy the announcement. In this way, the set of worlds (the epistemic state) becomes progressively restricted.

### Dynamic Broadcasts
In addition to predefined actions, the simulation implements a dynamic broadcast mechanism. At every tick, the simulation checks if an agent’s epistemic state has become uniform with respect to any of the propositions (i.e. every world in its current state satisfies a particular proposition such as contract being true). If so, and if the agent has not yet broadcast that fact, it schedules a broadcast for the next tick. This mechanism mimics the natural process of agents "learning" a fact completely and then informing their neighbors, which further synchronizes the knowledge across the network.

### Broadcast Update and Synchronization
After processing both scheduled and predefined actions at each tick, every agent broadcasts its complete epistemic state to its neighbors. Upon receiving this broadcast, each neighbor updates its state by taking the intersection with the broadcast states. This step is crucial for synchronizing the network; over time, the agents’ epistemic states converge.

## Visualization of the Combined Kripke Model
The simulation uses a combined Kripke model to visualize the epistemic state of the network at each tick. In this model:

- Nodes: Represent the eight fixed possible worlds, each labeled with the truth values of contract, a_contract, and b_contract.
- Edges (Arrows): For each agent, colored arrows (using a unique color per agent) are drawn between every pair of worlds that the agent still considers possible. Since the epistemic relation for an agent is complete over its set of possible worlds, every pair of nodes in that subset is connected.
The visualization helps to illustrate how the information propagated through the network restricts the agents’ epistemic states. Initially, the Kripke model shows all eight worlds with each agent’s accessibility relation covering all nodes. After successive broadcasts, the number of accessible worlds for each agent reduces. Ultimately, the model converges when every agent considers only the correct world (i.e. the world where all propositions are true).

Below are some example figures :

Reasoned for a couple of seconds
Below is an expanded version of the report text. You can include this in your final submission. It explains in detail the simulation design, the role assignment, the epistemic update process, and the visualization of the combined Kripke model.

Simulation of Epistemic Updates in a P2P Network
This simulation models how knowledge propagates and becomes synchronized in a peer-to-peer network through dynamic epistemic updates. The simulation is executed by calling the function:

python
Copy
epistemic_simulation(num_agents, num_ticks, p_connection)
where:

num_agents is the number of P2P agents (nodes) in the network,
num_ticks is the total number of simulation ticks (time steps), and
p_connection is the probability that any two agents are directly connected.
Overview
Initially, each agent is completely uncertain about the state of three propositions:

contract
a_contract
b_contract
This uncertainty is captured by assuming that each agent considers all eight unique possible worlds as possible. (These worlds represent every combination of truth values for the three propositions.) A fixed domain of eight worlds is defined and shared by all agents. Each agent’s epistemic state is represented as a subset of these worlds.

Random Role Assignment
At the beginning of the simulation, roles are randomly assigned:

Contract Owner: One agent is randomly selected as the contract owner. This agent is responsible for learning (and later broadcasting) that the contract exists.
Signer A and Signer B: Two different agents are randomly chosen from the remaining agents to act as the signers. Signer A will later broadcast that a_contract is true, and Signer B will broadcast that b_contract is true.
This random assignment ensures that the simulation is stochastic, so the roles and hence the subsequent flow of information may vary each time the simulation is run.

Propagation of Epistemic Updates
Predefined Epistemic Actions
At specific ticks, certain agents update their epistemic state with a predefined announcement. For example:

At tick 1 and tick 2, the contract owner updates its epistemic state with {"contract": True} and immediately broadcasts this fact to its direct neighbors.
At tick 3, Signer A broadcasts that {"a_contract": True}.
At tick 4, Signer B broadcasts that {"b_contract": True}.
When an agent receives a broadcast (whether predefined or dynamically scheduled), it updates its epistemic state by filtering out those worlds that do not satisfy the announcement. In this way, the set of worlds (the epistemic state) becomes progressively restricted.

Dynamic Broadcasts
In addition to predefined actions, the simulation implements a dynamic broadcast mechanism. At every tick, the simulation checks if an agent’s epistemic state has become uniform with respect to any of the propositions (i.e. every world in its current state satisfies a particular proposition such as contract being true). If so, and if the agent has not yet broadcast that fact, it schedules a broadcast for the next tick. This mechanism mimics the natural process of agents "learning" a fact completely and then informing their neighbors, which further synchronizes the knowledge across the network.

Broadcast Update and Synchronization
After processing both scheduled and predefined actions at each tick, every agent broadcasts its complete epistemic state to its neighbors. Upon receiving this broadcast, each neighbor updates its state by taking the intersection with the broadcast states. This step is crucial for synchronizing the network; over time, the agents’ epistemic states converge.

Visualization of the Combined Kripke Model
The simulation uses a combined Kripke model to visualize the epistemic state of the network at each tick. In this model:

Nodes: Represent the eight fixed possible worlds, each labeled with the truth values of contract, a_contract, and b_contract.
Edges (Arrows): For each agent, colored arrows (using a unique color per agent) are drawn between every pair of worlds that the agent still considers possible. Since the epistemic relation for an agent is complete over its set of possible worlds, every pair of nodes in that subset is connected.
The visualization helps to illustrate how the information propagated through the network restricts the agents’ epistemic states. Initially, the Kripke model shows all eight worlds with each agent’s accessibility relation covering all nodes. After successive broadcasts, the number of accessible worlds for each agent reduces. Ultimately, the model converges when every agent considers only the correct world (i.e. the world where all propositions are true).

Below are some example figures (replace the image URLs with your own assets if needed):

![image](https://github.com/user-attachments/assets/9b1cc46a-450c-4237-8702-6130fa17766a)
Figure 1. A randomly generated P2P network with random connections.

![image](https://github.com/user-attachments/assets/720f48ab-146e-4ef4-9493-cb23fb57adb5)
Figure 2. The initial Kripke model showing all eight possible worlds after the contract owner has learned and broadcast the contract.

![image](https://github.com/user-attachments/assets/bb092754-697f-4376-a349-c4ce1676d6ae)

Figure 3. The epistemic model becomes restricted as the simulation proceeds through successive ticks.

![image](https://github.com/user-attachments/assets/fe998c92-e69a-44dd-bbfe-b77dc1a4815b)
Figure 4. Final convergence: all agents consider the correct world where contract, a_contract, and b_contract are true.


