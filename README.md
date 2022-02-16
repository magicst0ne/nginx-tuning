NGINX Tuning For Best Performance
=================================
Our goal is that find a way improve the server's RPS.

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
- Version 4.2.0 of wrk running on the client machine generated the traffic that NGINX proxied. We installed it according to these instructions.
- Version 1.18.0 of NGINX Open Source ran on the web server machines. We installed it from the official package repository of Ubuntu according to these instructions.
- Ubuntu 20.04.3 LTS ran on both client and web server machines.

## Tuning Your Linux Configuration
The settings in modern Linux kernels (5.4.0-99-generic) are suitable for most purposes, but changing some of them can be beneficial. Check the kernel log for error messages indicating that a setting is too low, and adjust it as advised. Here we cover only those settings that are most likely to benefit from tuning under normal workloads. For details on adjusting these settings, please refer to your Linux documentation.
**The Backlog Queue**
- net.core.somaxconn = 4096
- net.core.netdev_max_backlog = 1024

**File Descriptors**
- sys.fs.file-max – The system‑wide limit for file descriptors
- nofile – The user file descriptor limit, set in the /etc/security/limits.conf file

**Ephemeral Ports**
- net.ipv4.ip_local_port_range = 32768 59000

## Tuning Your NGINX Configuration
**Worker Processes**
- worker_processes auto;
- worker_connections 10240;

**Keepalive Connections**
- keepalive_timeout 65;

**Access Logging**
- access_log off; 

**Sendfile**
- sendfile on;

## Performance Metrics and Analysis
RPS for HTTP Requests
The table and graph below show the number of HTTP requests for varying request sizes, in kilobytes (KB).
|  Request Sizes | RPS	 | CPU Usage	 | Traffic	 |
| :----:| ----: | ----: | ----: |
| 0.6 KB | 106165 | 100% | 821Mb/s |
| 1.2 KB | 74967 | 85.2% | 985Mb/s |
