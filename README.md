🦠 Emergent Molecular Communication
A comprehensive preliminary study of emergent molecular communication protocols learned by graph-based agents in a diffusion channel environment, integrated with Reinforcement Learning.

📋 Table of Contents
🦠 Emergent Molecular Communication

✏️ Abstract

✉️ Authors

⚙️ Installation

🚀 Usage

🧠 Reinforcement Learning for Adaptive Communication

🧪 MolComEnv: The Custom Gymnasium Environment

Observation Space

Action Space

Reward Function

🤖 RL Agent Training

📈 Evaluation and Visualization

✏️ Abstract
Biological organisms have developed sophisticated communication mechanisms to enhance their adaptability and survival, ranging from molecular signaling to complex linguistic structures. Understanding the evolution of these mechanisms can provide insights into both biological processes and artificial communication system design. As a first attempt in this direction, a preliminary system based on Graph Neural Networks (GNNs) and molecular diffusion models is presented in this paper to observe the emergence of Molecular Communication (MC) protocols among artificial agents. In particular, these agents interact according to a Lewis-game framework by exchanging molecules that diffuse in a fluidic environment. In this framework, a sender encodes and transmits symbols to a destination with the help of intermediate relay nodes, subject to the stochastic behavior of diffusion-based MC, which affects message integrity. Each of these nodes can tune its internal parameters to influence communication, mimicking the evolution of biological organisms such as bacteria. Preliminary numerical results suggest that this system can learn to evolve an effective MC protocol. The findings highlight the potential of such a system for investigating emergent MC, possibly leading to a better understanding of molecular biological systems and the optimization of bio-based and bio-inspired networked systems.

✉️ Authors
Alberto Archetti1

Gabriele Giusti1

Karthik R. Gorla1,3

Stefano Caputo2

Maurizio Magarini1

Matteo Matteucci1

Lorenzo Mucchi2

Massimiliano Pierobon3

1Department of Electronics, Information, and Bioengineering, Politecnico di Milano, Milan, Italy
2Department of Information Engineering, Università degli Studi di Firenze, Florence, Italy
3School of Computing, University of Nebraska–Lincoln, Lincoln, NE, USA

⚙️ Installation
Clone the repo:

git clone https://github.com/sas87f/commence-tmbc.git
cd commence-tmbc

Compile LaTeX Code

Create Conda environment:

conda env create -f environment.yml
conda activate commence

Compile LaTeX Code

Install Python dependencies:

poetry install

Compile LaTeX Code

🚀 Usage
Run the Jupyter notebook to train, evaluate, and collect metrics:

jupyter lab commence_model.ipynb

Compile LaTeX Code

🧠 Reinforcement Learning for Adaptive Communication
To enhance the adaptability of the molecular communication system in dynamic environments, a Reinforcement Learning (RL) framework has been integrated. The RL agent learns to make decisions that influence message propagation, aiming to optimize communication accuracy even when network conditions change (e.g., due to node failures). This setup allows the system to mimic the adaptive behavior observed in biological organisms.

🧪 MolComEnv: The Custom Gymnasium Environment
The core of the RL integration is MolComEnv, a custom environment built using the Gymnasium library. It simulates a molecular communication channel with dynamically changing conditions.

Network Interaction: At its heart, MolComEnv interacts with the MolComNetwork model, which orchestrates the diffusion-based message passing between nodes. This includes utilizing a pre-trained encoder (from the classification task) to transform input data into chemical messages.

Dynamic Node Failures: A key aspect of the environment is the introduction of stochastic node failures. Nodes can become inactive at the beginning of an episode or dynamically during a step, providing a challenging and realistic scenario for the RL agent to adapt to.

Device Handling: The environment is configured to properly move tensors and the MolComNetwork model to the specified device (CPU or CUDA) for efficient computation.

Observation Space
The agent perceives the environment through a dictionary-based observation space, providing comprehensive information about the network's state:

messages (spaces.Box): A continuous array representing the current concentration or state of chemical messages at each node. Its shape is (n_nodes, n_classes), where n_classes is the dimensionality of the chemical message (typically derived from the number of classes in the underlying classification task). This allows the agent to gauge the signal strength and composition across the network.

active_nodes_mask (spaces.MultiBinary): A binary vector of shape (n_nodes,) indicating the operational status of each node (1 for active, 0 for failed). This is crucial for the agent to understand the current network topology and identify potential communication bottlenecks.

Action Space
The agent's decisions are represented by a spaces.MultiBinary vector of shape (n_nodes,). Each element in this vector corresponds to a specific node in the communication graph:

A value of 1 for a node indicates that the agent "activates" or "strengthens" its relaying capabilities for the current message.

A value of 0 suggests the node's relaying is "deactivated" or "weakened".

These actions directly influence the relay_strength applied to messages at each node during the message passing process, allowing the agent to dynamically control signal propagation.

Reward Function
The reward system is carefully designed to guide the agent towards efficient and robust message delivery:

Positive Reward for Classification Accuracy: A base reward of +10.0 is given if the message, after propagation, leads to a correct classification of the original input data at the receiver node. This encourages successful information transfer.

Penalty for Inactive Nodes: A small penalty (-0.1 per inactive node) is applied for each node that the agent effectively "turns off" (i.e., sets its relay_strength to 0). This discourages unnecessary deactivation of potentially useful relay points and promotes network utilization.

Large Penalty for Receiver Failure: A significant negative reward of -5.0 is imposed, and the episode terminates, if the receiver node itself fails. This strongly penalizes failures that directly impede the primary goal of communication.

Terminal Bonus: A substantial bonus of +50.0 is awarded at the end of an episode if the final classification at the receiver is correct. This emphasizes the importance of end-to-end communication success over the entire duration of the message propagation.

The environment's reset() method initializes a new communication scenario, including a fresh message and a potential initial node failure. The step() method processes the agent's chosen action, simulates one iteration of molecular message passing, updates the environment's state, and calculates the corresponding reward.

🤖 RL Agent Training
The RL agent is trained using the Proximal Policy Optimization (PPO) algorithm, a widely adopted and robust policy-gradient method implemented via the Stable Baselines3 library.

Policy Architecture: Given the dictionary-based observation space, a MultiInputPolicy is employed, which is adept at handling structured input observations.

Training Process: The agent learns by interacting with multiple parallel instances of the MolComEnv (configured via make_vec_env) over a specified number of total_timesteps (e.g., 1,000,000). During this process, it refines its policy to select optimal node activation strategies to maximize cumulative reward.

Hyperparameters: Key hyperparameters such as learning_rate (e.g., 1e-4) and gamma (discount factor, e.g., 0.99) are configured to control the learning dynamics. These can be tuned for optimal performance based on experimentation.

Logging: TensorBoard integration (tensorboard_log="./ppo_molcom_log/") facilitates comprehensive monitoring of the training progress, including various metrics like rewards, losses, and value estimates.

📈 Evaluation and Visualization
Following the training phase, the performance of the learned RL policy is rigorously evaluated over a set number of num_eval_episodes (e.g., 50). During evaluation, the agent operates in a deterministic mode (disabling exploration) to provide an unbiased measure of its learned capabilities. The total reward accumulated in each episode serves as a direct indicator of how effectively the trained agent ensures robust communication in the presence of node failures.

The plot_rl_evaluation_rewards utility function is used to visualize the agent's performance during evaluation, optionally applying smoothing to the reward curve for better trend analysis. Additionally, a conceptual plot_node_activity_heatmap is available, which, if integrated into the environment's data collection, could provide valuable insights into the agent's dynamic node activation strategies over time.