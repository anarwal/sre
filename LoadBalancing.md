Load Balancing Algorithms:
- Random: Uses random number generator and forwards the call randomly based on that.
- Round Robin: Using a circular queue, load balancer walks through it. Sending one request per server
- Weighted round robin: New web servers are assigned higher weight whereas old one are provided lower weight, Load balancer send more traffic to the ones with higher weight
- Dynamic Round robin: dynamically weight is generated and if two have same then based on round robin request is forwarded
- Fastest: Load balancer forward based on shortest response time
- Least connections: Load balancer forward based on least number of connections
- Observed: combination of fastest and least connections
- Predictive: Based on observed, it predicts which one will behave better
