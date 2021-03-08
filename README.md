# MySQL
## Make MySQL Group Repliation more robust and stable

## Problems solved：
1. Solve performance jitter caused by the certification garbage collection.
2. Solve performance jitter caused by flow control module
3. Solve performance jitter caused by XCOM in order to be more tolerant and robust in the following scenarios:
   * A full partition is met
   * When one node is crashed
   * Network jitter is met
4. Modify Multi-write conflict detection's processing process in order to solve data lost problems
5. Support large transactions more friendly.
6. Solve TCP self-connect problems.
7. Change the behavior for after consistency level
   The transaction will wait until its changes have been applied on a majority of the members in a group in order to avoid performance collapse.
8. Improve the start process when the state is recovering 
9. Fix the whole cluster's performance collapse when the disk is full
10. Fix lots of thread synchronization problems for Group Replication consistency when view is changed.
11. Improve performance for BEFORE consistency level.
12. Accelate automatic primary election.
13. Detect network condition more accurately
14. Add arbitrator actor for Paxos communication
15. Improve message passing more smoothly.
16. Fix thread synchronization problems when staring

## Bugs and feature requests:
I hope that you're able to try out the latest version.
If you encounter any issues with the release, I would encourage you to file a bug report.
Your feedback is really critical to myself and the rest of the team as we want to make Group Replication better.
