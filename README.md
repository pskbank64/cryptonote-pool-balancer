# cryptonote-pool-balancer

A load balancer for cryptonote pools

## Motivation

### Increased scalability
With a proper, cryptonote protocol aware, balancer it will be easier for individual pool admins to spin up new pool servers to serve a higher load of miners on the same pool address. The miner ID can be used to route all RPCs from one miner to a specific pool server instance. 

### Improve load sharing across existing pools: regional loadbalancers
When you look at the www.sumopools.com you will see that the top pools have a very high miner load whereas other pools are almost idle. The official pool (pool.sumokoin.com) indicates that it is saturated and it would be better for all miners on that pool when some of the load from this pool would end up on the idle pools. 

Regional pool loadbancers could be used to distribute miners across existing pools within a region.

### Ensure miners connect to healthy pool servers
Today, when a pool server becomes unhealthy; a miner will not be able to continue it's work until the pool is fixed or the miner is reconfigured to run against a different pool. The pool balancer will perform periodic health checks (to be implemented in cryptonote-sumokoin-pool) to ensure that the pool is healthy. 
The health checks will make sure that:

 * The pool has a healthy connection with the wallet RPC
 * The pool has a healthy connection with the sumokoind RPC
 * RPC response time latency doesn't exceed a threshold.

If a pool is nolonger healthy; the balancer will direct the miner to a different pool.


