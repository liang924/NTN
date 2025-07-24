## System-Level Evaluation of Beam Hopping in NR-Based LEO Satellite Communication System
[Reference](https://arxiv.org/pdf/2205.10721)

-It provides insights into various beam hopping algorithms suitable for LEO satellites, which can enhance resource allocation efficiency and interference management in 5G NTN systems.

| Beam Hopping Strategy                  | Description                                                                 | Features                                                                                 | Performance Summary                                     |
|----------------------------------------|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------------|---------------------------------------------------------|
| Round Robin Scheme                     | A basic benchmark method that illuminates beams in a fixed rotating order. | - Ignores user traffic demands<br>- No interference avoidance                           | Lowest performance among all three schemes.            |
| Proposed Scheme without Distance Limit | Dynamically allocates beams based on traffic demand.                       | - Considers traffic demand<br>- May cause adjacent beams to be illuminated simultaneously | Better throughput but suffers from inter-beam interference. |
| Proposed Scheme with Distance Limit    | Optimized beam hopping with traffic awareness and spatial separation.      | - Considers traffic demand<br>- Avoids interference by not illuminating adjacent beams   | Best performance in terms of throughput and UE satisfaction. |

## Multi-Satellite Beam Hopping and Power Allocation Using Deep Reinforcement Learning
[Reference](https://arxiv.org/pdf/2501.02309)

| Beam Hopping Strategy | Description | Features | Performance Summary |
|------------------------|-------------|----------|----------------------|
| SAC (Soft Actor-Critic) | Uses deep reinforcement learning to learn optimal beam hopping and power allocation strategies through training over multiple networks. | Learns from environment, adapts to dynamic traffic and delays, multi-objective optimization. | Achieves the best overall performance in throughput, delay, and fairness due to intelligent decision-making. |
| Throughput Priority Beam Hopping (TP-BH) | Selects K cells with the highest traffic queues at each time slot. | Simple, queue-length based, serves areas with highest data demand. | Improves total throughput but may neglect delay-sensitive users. |
| Delay Priority Beam Hopping (DP-BH) | Selects K cells with the highest service delays to minimize system delay. | Delay-focused, distributes power to long-waiting users. | Reduces delay effectively but may not maximize total throughput. |
| User Service Weight Gain Priority Beam Hopping (USWGP-BH) | Calculates a combined service weight from traffic and delay, then selects top K cells. | Balances traffic load and delay, improves user experience. | Performs well in balancing efficiency and fairness, suitable for mixed-service environments. |

- SAC (Soft Actor-Critic) : Using Deep Reinforcement Learning, the SAC algorithm autonomously learns the optimal beam hopping and power allocation strategies under a multi-satellite, multi-beam architecture.
- All compared strategies are applied in NTN scenarios with multiple satellites and beams, serving as baselines:
  - TP-BH: selects beams based on traffic load
  - DP-BH: selects beams based on waiting time (delay)
  - USWGP-BH: considers both traffic and delay to balance efficiency and fairness
