# RustScan - Too noisy for a security tool

I have chosen RustScan for my personal fix.  It is primarily written in Rust (which I have a current personal affinity towards, and want to keep learning), coupled with the development Information Security solutions, made it a particularly interesting project for me. This seems to be the perfect project for me to understand and develop offensive security tools in Rust, which was one of my main goals for this course. I might even continue contributing as it is directly in line with my interest.

[RustScan](https://github.com/RustScan/RustScan) is a network scanner, providing extremely fast, and efficient Rust-based port scanning. The current industry standard is [nmap](https://nmap.org/) which is written in C but  can be considered somewhat of a legacy; slower tech-stack than what is being used today. The reason Rust is perfect for this is because Network Scans can take an exorbitant amount of time, and are vastly different for various networking setups. Speed, and efficiency is key in this process. So far, this seems to be the only, “best” popularly adopted Rust solution

This is a promising code-base for me since the creator is a fellow hacker (bee-san https://github.com/bee-san ) who does Security @ Duo, and is an open source project not attached to a larger company or foundation that a lot of other hackers have contributed to. I am all for open-source software that is not funded/fueled by evil. This is a live and active project with a lot of contributors, some of them are bots but there are about 5-10 people who have made considerable contributions. There is also extensive documentation that I can refer to, not just for usage, but for understanding the design, logic, and coding choices.

The biggest complaint is that RustScan is too noisy. Specifically this issue on Github:[https://github.com/RustScan/RustScan/issues/42](https://github.com/RustScan/RustScan/issues/42). 

This issue, which the creator themselves opened in 2020, is a long standing issue that is a core feature for any network scanner, and has still has not been implemented which gives me incentive to contribute. Contributors also highlight the importance of this issue and give some solutions. No fix has been attempted before. The lack of interval control leads to a high request frequency, often triggering network-based intrusion detection systems (NIDS) or firewall blocks. This problem becomes even more apparent in complex or heavily monitored environments, where rapid scanning can alert or overwhelm the system's defenses. Implementing intervals will allow RustScan to adapt to more realistic network conditions, offering an approach that is both efficient and evasive, aligning with techniques used in real-world offensive security.
  
To address this noise issue, I plan to implement a feature that allows users to set intervals between scans on each port. This way, we are only checking 1 port at a time with TIMEOUT delay, but because we are checking them across every IP it should run in the same time, but be less noisy to a specific single server.  

The solution I propose will involve creating an `--interval` option that allows users to define the delay between each port scan request, thus decreasing the overall frequency and making the scan appear less aggressive. This pseudocode, currently scans each IP address and then checks every port will implement a sleep function or some other time-based logic. This will pace each scan according to user preference. 
  
```
for every IP address:
  for every port in port_list:
    check port
    sleep(interval)
```

This approach achieves a quieter, more adaptive scan and allows RustScan to compete effectively with tools like nmap in terms of precision and configurability. Given the security community’s emphasis on stealthy and non-intrusive testing, I believe this feature could significantly expand RustScan’s utility and adoption.
