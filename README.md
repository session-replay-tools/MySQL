# MySQL Group Replication Download
## Make MySQL Group Replication more robust and stable

## The following problems are resolved：
1. Solve performance jitter caused by the Certification garbage collection.
   * A new data structure is designed in order to collect garbage more effectively and quickly. 
2. Solve performance jitter caused by flow control module.
   * A total different algorithm is designed in order to reduce memory and control the flow more accurately and smoothly.
3. Solve performance jitter caused by XCOM in order to be more tolerant and robust in the following scenarios:
   * A full partition is met
   * When one node is crashed
   * Network jitter is met
4. Modify Multi-write conflict detection's processing procedure in order to solve data lost problems.
5. Support large transactions more friendly.
   * A more intelligent algorithm is designed to make a fair judgement.  
6. Solve TCP self-connect problems.
   * No more strange events for deploying group members in the same machine.
7. Change the behavior of after consistency level for following majority rule
   * The transaction will wait until its changes have been applied on a majority of the members in a group in order to avoid performance collapse when network partition is met.
8. Improve the start process when all group members are started at the same time.
   * This modification avoids the dead state of all members which are all in recovering state.
9. Fix the whole cluster's performance collapse when the disk is full.
   * When one disk is full, the whole cluster could possibly enter a dead state.
10. Fix lots of thread synchronization problems for Group Replication consistency when view is changed.
   * A lot of horrible errors could occur when one member is joined.
11. Improve performance for BEFORE consistency level.
   * This modification could improve performance significantly for consistent reading
12. Accelerate automatic primary election.
   * Change from original about 30 seconds to about 7~13 seconds according to failure type. It should be noted that group_replication_member_expel_timeout takes up 5 seconds by default.
13. Detect network conditions more accurately.
   * When one member is crashed,  one second is needed to detect this failure instead of official 5 seconds.
14. Add arbitrator mode for Paxos communication.
   * The arbitrator member does not store any data and only participates in vote.
15. Improve message passing more smoothly.
   * Batch size is limited to 65536 in order to avoid  inefficiently message passing.
   * Send less data at a time in order to avoid performance jitter.
16. Fix thread synchronization problems when staring Group Replication.
17. A lot of other problems which occur very rarely are not described for clarity.

## Note:
1. The tar.xz file only works for Centos 7+ version
2. As the flow control algorithm is total different, the modified version is not compatible with the official version
3. slave_parallel_workers should be set twice the CPU number in order to achieve better performance.
4. For using arbitrator, set loose-group_replication_arbitrator=true
5. The new flow control algorithm uses group_replication_flow_control_replay_lag_behind variable which default value is 60 seconds for flow control. If you want to do write test only, you should set group_replication_flow_control_replay_lag_behind larger.

## Bugs and feature requests:
If you encounter any issues with the release, I would encourage you to file a bug report.
Your feedback is really critical to myself and the rest of the team as we want to make Group Replication better.
