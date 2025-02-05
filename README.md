## What is a blockchain. 
A blockchain is a decentralized digital ledger that records transactions across a network of computers. Unlike traditional ledgers maintained by a single controlling authority, blockchain technology is distributed across multiple nodes, each of which keeps a copy of the entire ledger. Whenever a new transaction is added, it must be verified and agreed upon by a consensus mechanism—often based on algorithms like Proof of Work or Proof of Stake—before being incorporated into a new “block” that is appended to the chain of existing blocks. This decentralized structure enhances transparency and security because every participant can see the same record, making it extremely difficult for malicious actors to alter or falsify transactions without detection.

One of the key innovations of blockchain lies in its ability to create trust in a trustless environment. Participants, who may not necessarily know or trust each other, can carry out transactions with confidence that the system’s rules and cryptographic safeguards prevent tampering. Beyond cryptocurrencies like Bitcoin and Ethereum, blockchain technology is finding applications in supply chain management, finance, healthcare, and various other fields where transparency, immutability, and resilience against single points of failure are paramount. As the technology evolves, it continues to show promise for reshaping how organizations and individuals share information and conduct business on a global scale.
## P2P network
In a blockchain’s peer-to-peer (P2P) network, each node (or participant) connects to a subset of other nodes rather than every single one, creating a loosely connected topology instead of a fully connected mesh. This means that while no single node is directly linked to all others, the network as a whole can still efficiently broadcast transactions and blocks by passing information from one peer to the next. This decentralized structure reduces bottlenecks and single points of failure, as no central server is in charge of coordinating network activity. By relying on multiple, overlapping connections among subsets of peers, the network remains resilient: if one route is compromised, there are typically alternate paths available to keep communication flowing. Consequently, the P2P architecture ensures that updates—such as new transactions—can propagate to every node over time, helping maintain a consistent, tamper-resistant ledger across all participants.
## What is Kaspa and GhostDAG

Kaspa is a proof-of-work (PoW) cryptocurrency that emphasizes speed, scalability, and security by leveraging an innovative consensus mechanism known as GHOSTDAG. While it retains core principles from Bitcoin—like decentralized validation and immutability—Kaspa aims to solve the scalability and throughput limitations often associated with traditional blockchain networks. By producing blocks on the order of seconds, Kaspa enables a higher transaction rate without significantly compromising network security. This faster block generation is made possible by an underlying architecture that accommodates parallel block creation while maintaining a secure, coherent ledger.

At the heart of Kaspa lies GHOSTDAG (Greedy Heaviest Observed SubDAG), a consensus algorithm that generalizes Nakamoto Consensus to handle faster block rates and higher transaction throughput. Under traditional Nakamoto Consensus, nodes always choose the "longest chain" of blocks as the valid ledger. GHOSTDAG extends this concept by considering not just a single chain of blocks, but rather a directed acyclic graph (DAG) of blocks that can include multiple, competing branches. This approach recognizes and orders all blocks—even those that would typically become "orphans" in a typical longest-chain setup—thus utilizing a greater share of network bandwidth. As a result, the network can accept and merge blocks from different miners almost simultaneously, increasing overall efficiency and reducing wasted work on stale blocks.

The use of GHOSTDAG offers several advantages over legacy blockchains reliant on strict linearity. By allowing blocks to coexist and then resolving their order through a DAG-based mechanism, Kaspa achieves faster confirmations without sacrificing the fundamental security assumptions that underpin Bitcoin’s Nakamoto Consensus. It effectively balances block propagation and chain security, ensuring the network remains resistant to double-spending and various attack vectors. This generalization of Nakamoto’s longest-chain rule into a heaviest-subDAG paradigm sets the stage for future blockchains to scale without forfeiting the cryptographic and economic properties that define decentralized ledger security.
# Why action models

Action models, as used in dynamic epistemic logic, provide a flexible framework for representing how agents update their knowledge in environments where information is distributed unevenly—such as in a peer-to-peer (P2P) network. Unlike public announcements that assume instantaneous and global knowledge updates, action models capture the nuances of asynchronous communication and partial connectivity. In a P2P network, not every agent is connected to every other agent, and messages or actions may only be visible to a subset of the network. This means that when an event occurs (for example, a miner embedding data in a block), only agents directly connected to that miner update their knowledge. The unconnected agents, unable to distinguish this specific update from any other, remain unaware, thereby reflecting the realistic delays and localized information flow in such networks.

Consider three propositional atoms in our scenario:

- **contract:** an agent’s knowledge about the existence of the contract,
- **a_contract:** agent _a_’s intention to sign the contract, and
- **b_contract:** agent _b_’s intention to sign the contract.

The true state of the world is that all three atoms are true (i.e., the contract exists and both agent _a_ and agent _b_ want to sign it). However, at the outset, no agent is aware of these truths; each assumes that ¬contract, ¬a_contract, and ¬b_contract hold. To model how this knowledge is disseminated over time in the network, we can define several action models. For example, the **first action model** simulates the embedding of the contract in a block by a miner. In this model, when the miner updates the blockchain with the contract, only agents connected to this miner update their epistemic state to reflect the fact that _contract_ is true. Agents not connected to the miner cannot distinguish this action from other actions; for them, it appears as an indistinguishable, uninformative event.

Building on that, the **second action model** represents the scenario where agent _a_ broadcasts the existence of the contract to all of its direct connections. The precondition for this action is that agent _a_ must already know about the contract (i.e., the precondition is _contract_). Once the broadcast is made, all agents directly connected to _a_ update their knowledge and recognize that _contract_ holds. Again, for any agent not connected to _a_, this broadcast is not discernible from a generic action—emphasizing the localized spread of information. Similarly, the **third action model** captures the situation where agent _a_ declares its intention to sign the contract, thus updating its state to _a_contract_. The precondition here is also that agent _a_ must know about the contract. Upon this action, the connected agents become aware of agent _a_’s intent to sign, while those out of the connection range remain oblivious. (A fourth action model, mirroring the third, could similarly be defined, reinforcing that such actions remain local to the network segment connected to agent _a_.)

In summary, these action models illustrate how knowledge can be distributed in a P2P network with delays and partial connectivity. By specifying both the preconditions (e.g., an agent must know that the contract exists before announcing or signing it) and the visibility relations (only connected agents perceive the specific update), action models capture the real-world dynamics of decentralized systems far more effectively than global public announcements. This makes them an ideal tool for modeling and analyzing knowledge distribution in blockchain networks and other distributed environments.

# Action Models 

##### **Action Model 1:** Miner Embeds the Contract in a Block

**Events**: $E = \{e_m , e_d\}$, where $e_{m}$ is the event where the miner embeds the contract and $e_d$ is the event where the other agents do not distingush the event from not embedding the contract, since it is not broadcastted yet. 

**Relations**: $e_m \sim e_d$ , the two events are the same for all of the other miner/agents

**Precondition**
$pre(e_m) = contract$

##### **Action Model 2:** Agent a Broadcasts existense of the Contract

Here, agent _a_ tells all its direct connections that the contract exists. Only agents connected to _a_ receive the actual announcement.

Events: $E = \{e_c , e_d\}$, where $e_{c}$ is the event where the miner the broadcast the knowlege about the contract and $e_d$ is the event where the other agents do not distingush the event.

**Relations:** $e_c \sim_{i} e_d$ if and only if agent i is not connected to agent a.

Precondition
$pre(e_c​)=contract$, (the agent can only broadcast the contract if it already knows about it)


##### **Action Model 3**: Agent _a_ Announces Its Intention to Sign the Contract 
In this update, agent _a_ declares, “I want to sign the contract” (i.e. asserts a_contracta\_contracta_contract). Only its neighbors learn about this intention.

**Events**: $E = \{e_{a_{sign}} , e_d\}$, where $e_{a_{sign}}$ is the event where the agent says that they know they want to sign the contract and, $e_d$ is the dummy event that cannot be distiguished by other non connected agents.

**Relations:** ${e_{a_{sign}}} \sim e_d$ if and only if agent i is not connected to agent a, and *i* is part of the set of agents and i != a.

**Precondition**
$pre({e_{a_{sign}}}​)=contract$, (know the contract exists before announcing that its knows it wants to sign.)

##### **Action Model 4: Agent _b_ Announces Its Intention to Sign the Contract 
In this update, agent _b_ declares, “I want to sign the contract” (i.e. asserts a_contracta\_contracta_contract). Only its neighbors learn about this intention.

**Events**: $E = \{e_{b_{sign}} , e_d\}$, where $e_{a_{sign}}$ is the event where the agent says that they know they want to sign the contract and, $e_d$ is the dummy event that cannot be distiguished by other non connected agents.

**Relations:** ${e_{b_{sign}}} \sim_{i} e_d$ if and only if agent i is not connected to agent b , and *i* is part of the set of agents and i != b.

**Precondition**
$pre({e_{a_{sign}}}​)=contract$, (know the contract exists before announcing that its knows it wants to sign.)


##### **Action Model 5: Agent gives all of its knowledge to its connections 
In this update, agent _b_ declares, “I want to sign the contract” (i.e. asserts a_contracta\_contracta_contract). Only its neighbors learn about this intention.

**Events**: $E = \{e , e_d\}$, where e is the event in which the agent comunicates $\phi$ ,its knowledge and $e_d$ is the dummy event that cannot be distiguished by other non connected agents.

**Relations:** $e \sim_{i} e_d$ if and only if agent i is not connected to the agent executing the event, and *i* is part of the set of agents and i != a.

**Precondition**
$pre(e)=pre(e_{d}​)=ϕ$, This means that the broadcast action can only be applied in worlds where φ is true.
