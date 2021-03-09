# MySQL
## Make MySQL Group Repliation more robust and stable

## Problems solved：
1. Solve performance jitter caused by the certification garbage collection.
2. Solve performance jitter caused by flow control module.
3. Solve performance jitter caused by XCOM in order to be more tolerant and robust in the following scenarios:
   * A full partition is met
   * When one node is crashed
   * Network jitter is met
4. Modify Multi-write conflict detection's processing procedure in order to solve data lost problems.
5. Support large transactions more friendly.
6. Solve TCP self-connect problems.
7. Change the behavior of after consistency level
   * The transaction will wait until its changes have been applied on a majority of the members in a group in order to avoid performance collapse when network partition is met.
8. Improve the start process when the node state is recovering.
9. Fix the whole cluster's performance collapse when the disk is full.
10. Fix lots of thread synchronization problems for Group Replication consistency when view is changed.
11. Improve performance for BEFORE consistency level.
12. Accelate automatic primary election.
13. Detect network conditions more accurately.
14. Add arbitrator mode for Paxos communication.
15. Improve message passing more smoothly.
16. Fix thread synchronization problems when staring Group Replication.

## Note:
1. The tar.xz file only works for centos 7+ version
2. As the flow control algorithm is total different, the modified version is not compatible with the official version
3. slave_parallel_workers should be set two twice the cpu number in order to achieve beffer performance.
4. For using arbitrator, set loose-group_replication_arbitrator=true
5. The new flow control algorithm uses group_replication_flow_control_replay_lag_behind variable which default value is 60 seconds for flow control. If you want to do write test only, you should set group_replication_flow_control_replay_lag_behind larger.

## Bugs and feature requests:
If you encounter any issues with the release, I would encourage you to file a bug report.
Your feedback is really critical to myself and the rest of the team as we want to make Group Replication better.
