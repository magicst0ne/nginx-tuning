NGINX Tuning For Best Performance
=================================
Our goal is that find a way improve the server's QPS.

## Testing Overview
All tests were done using three separate machines connected together with 1 GbE links in a simple, flat Layer 2 network.
To generate traffic from the client machine, we used a performance testing tool. 


## Hardware Used
**We used the following hardware for the testing on both client and web server machine:**
- CPU: Intel(R) Core(TM) i5-4278U CPU @ 2.60GHz
- Network: BCM57766 Gigabit Ethernet PCIe (rev 01) 
- Memory: 8GB

## Software Used
**We used the following software for the testing:**
go-stress-testing
- Version 4.2.0 of wrk running on the client machine generated the traffic that NGINX proxied. We installed it according to these instructions.
- Version 1.18.0 of NGINX Open Source ran on the web server machines. We installed it from the official package repository of Ubuntu according to these instructions.
- Ubuntu 20.04.3 LTS ran on both client and web server machines.

## Performance Metrics and Analysis
|  Request Sizes | Rps	 | CPU Usage	 | Traffic	 |
| :----:| ----: | ----: | ----: |
| 0.6 KB | 106165 | 100% | 821Mb/s |
| 1.2 KB | 74967 | 85.2% | 985Mb/s |
