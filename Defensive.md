## Blue Team: Summary of Operations

### Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior

### Network Topology
The following machines were identified on the network:
- Azure VM
   - Operating System: Microsoft Azure 
   - Purpose: Host 
   - IP Address: 192.168.1.100:5601/
- Kali
   - Operating System: Kali Linux
   - Purpose: Use to attack other machines.
   - IP Address: 192.168.1.90
- Capstone
   - Operating System: Ubantu
   - Purpose: Testing target machine that will forward logs to ELK machine. 
   - IP Address: 192.168.1.105
- ELK
   - Operating System: Linux
   - Purpose: Seting Kibana Alert
   - IP Address:192.158.1.100
- Target 1
   - Operating System: Debian/Linux 
   - Purpose: Target machine for the final project.
   - IP Address: 192.168.1.100
- Target 2
   - Operating System: Debian
   - Purpose:Target machine for the final project.
   - IP Address: 192.168.1.115

### Description of Targets
The target of this attack was: Target 1 (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets
Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

### Excessive HTTP Errors
Excessive HTTP Errors is implemented as follows:
   - Metric: Metricbeat
   - Threshold: Status code above 400 more than 5 times in the past minute. 
   - Vulnerability Mitigated: wpscan bruteforce
   - Reliability: High reliability.

### HTTP Request Size Monitor
HTTP Request Size Monitor is implemented as follows:
   - Metric: Metricbeat
   - Threshold: http.request.bytes are over 3500
   - Vulnerability Mitigated: Monitor a The content-length header gives the size (in bytes) of the response body.
   - Reliability: Medium reliability.

### CPU Usage Monitor
CPU Usage Monitor is implemented as follows:
   - Metric: Metricbeat
   - Threshold: max system.process.cpu.total.pct is above 0.5 
   - Vulnerability Mitigated: privilege escalation/ consistent system usage.
   - Reliability: High reliability.

### SSH activity monitor
SSH activity monitor is activity on target1/server is implemented as follows:
   - Metric: filebeat
   - Threshold:  when count Grouped over top 5 ‘system.auth.ssh.event is above 0 for last 5 seconds
   - Vulnerability Mitigated: Unknown individuals that successful SSH into server.
   - Reliability: Medium reliability.

### Command Line Process Monitor
Command Line Process Monitor is implemented as follows:
   - Metric: metricbeat
   - Threshold: When Count() GROUPED OVER Top 10 ‘process.comman_line’ IS ABOVE 5 FOR THE LAST 5 minutes
   - Vulnerability Mitigated: Privilege escalation 
   - Reliability: medium reliability.

### ICMP request Code monitor
ICMP Request Code implemented as follows:
   - Metric: packetbeat
   - Threshold: when count() GROUPED OVER top 100 ‘icmp.request.code’ IS ABOVE 10 5FOR THE LAST 3 minutes
   - Vulnerability Mitigated: NMAP/vulnerability scans using icmp
   - Reliability: medium reliability.
