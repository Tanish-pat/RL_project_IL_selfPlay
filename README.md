# Single Player Self Play with Imitation Learning

This project presents an Imitation Learning-Guided Self-Play Framework tailored for single-agent reinforcement learning (RL) environments, with Gymnasium's LunarLander-v3 as the benchmark task. The agent iteratively refines its policy by first leveraging expert demonstrations and subsequently through a novel self-play paradigm.

The pipeline is initiated by training a Deep Q-Network (DQN) model to serve as the expert policy. The modular architecture allows seamless integration of external expert models—provided consistent naming conventions are followed—thus removing the dependency on local expert training.

The initial policy learning is bootstrapped via Imitation Learning, starting with Behavior Cloning (BC). If BC underperforms, the framework transitions to the more robust Dataset Aggregation (DAgger) algorithm to improve generalization and mitigate covariate shift.

Following imitation, the agent engages in a single-agent self-play loop implemented via one of two mechanisms:

- Multi-Round, Multi-Model Optimization: Multiple agent instances play parallel episodes, with performance aggregated through a multi-objective optimization function (fully specified in the accompanying technical report). This fosters diverse policy exploration and robustness.

- Monte Carlo Tree Search (MCTS)-Guided Policy Iteration: Inspired by AlphaGo Zero, this approach integrates MCTS into policy improvement cycles. Each action is selected based on simulated rollouts and tree backups, favoring trajectories that yield higher long-term rewards. This enables sample-efficient exploration and policy refinement in a model-free setting.
