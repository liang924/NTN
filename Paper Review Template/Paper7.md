## System-Level Evaluation of Beam Hopping in NR-Based LEO Satellite Communication System
[Reference](https://arxiv.org/pdf/2205.10721)

-It provides insights into various beam hopping algorithms suitable for LEO satellites, which can enhance resource allocation efficiency and interference management in 5G NTN systems.

| Beam Hopping Strategy                  | Description                                                                 | Features                                                                                 | Performance Summary                                     |
|----------------------------------------|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------------|---------------------------------------------------------|
| Round Robin Scheme                     | A basic benchmark method that illuminates beams in a fixed rotating order. | - Ignores user traffic demands<br>- No interference avoidance                           | Lowest performance among all three schemes.            |
| Proposed Scheme without Distance Limit | Dynamically allocates beams based on traffic demand.                       | - Considers traffic demand<br>- May cause adjacent beams to be illuminated simultaneously | Better throughput but suffers from inter-beam interference. |
| Proposed Scheme with Distance Limit    | Optimized beam hopping with traffic awareness and spatial separation.      | - Considers traffic demand<br>- Avoids interference by not illuminating adjacent beams   | Best performance in terms of throughput and UE satisfaction. |
