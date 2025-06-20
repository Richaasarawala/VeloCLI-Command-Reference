# --cluster_rebalance [rebalance_type]

## Description
This command is executed on a VeloCloud Hub Edge within a cluster to initiate a re-distribution of its connected spoke Edges. The goal is to achieve a more uniform distribution of spokes across the Hubs in the cluster. The rebalance behavior depends on the specified `rebalance_type`.

## Arguments
| Argument        | Description                                                                                                                                                              |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rebalance_type`  | Specifies the mode of cluster rebalancing. This argument is mandatory. Valid values are:<ul><li>`include-self`: Triggers a rebalance operation aiming for a uniform distribution of spoke Edges across all Hubs in the cluster, including the Hub Edge where the command is executed.</li><li>`exclude-self`: Triggers a rebalance operation where the Hub Edge executing the command attempts to offload its connected spoke Edges to other Hubs in the cluster. This aims for a uniform distribution of spokes among the *other* Hubs.</li></ul> |

## Example usage
The example below shows the help output displayed when the mandatory `rebalance_type` argument is omitted.

```
example_com:velocli> debug --cluster_rebalance
usage: debug.py [-h] [--mode_link] [--timeout TIMEOUT SECONDS]
                [--logfile LOGFILE] [--limit N] [-v]
                [--biz_pol_dump [[all | segment-id] [[all | policy-name]
                ...]]] [--netflow_intervals] [--netflow_collectors]
                [--netflow_filters [<collector_id>]] [--bw_testing_dump]
                [--chat_stats [[sip=] [dip=] [dport=] [app_id=]
                ... (other debug options) ...
                --cluster_rebalance [rebalance_type]
                ...
debug.py: error: argument --cluster_rebalance: expected one argument
```

To trigger a rebalance that includes the current Hub in the distribution:
```
example_com:velocli> debug --cluster_rebalance include-self
Cluster rebalance initiated with include-self.
```

To trigger a rebalance that excludes the current Hub, offloading its spokes:
```
example_com:velocli> debug --cluster_rebalance exclude-self
Cluster rebalance initiated with exclude-self.
```
*(Note: The exact output messages for successful initiation may vary.)*

## Field descriptions
This command does not produce tabular output. Upon successful execution, it typically returns a confirmation message indicating that the cluster rebalance process has been initiated. The actual rebalancing process occurs in the background.