# RustScan Port Scan Interval Feature Implementation

# See Pull Request [here](https://github.com/RustScan/RustScan/pull/713)

This implementation adds a new feature to RustScan that allows users to specify a time interval between port scans, helping to control scan timing and potentially reduce network load. 


### 1. Command Line Arguments 
Added a new CLI argument for scan interval:

```rust 
/// Scan interval per port (in seconds)
#[structopt(long, default_value = "0")]
pub interval: u64,
```

### 2. Scanner Struct & Constructuor Modification
```rust
Copypub struct Scanner {
    interval: Duration,
}
Copyimpl Scanner {
    fn new(
        interval: Duration,
    ) -> Self {
        Self {
            interval,
        }
    }
}
```
### 3. Scanning Logic Modification

Changed from batch scanning to sequential port scanning
For each port:

- Scans the port across all IPs simultaneously
- Waits for all IPs to complete
- Applies the interval delay before moving to the next port

```rust
// Scan one port at a time
for port in ports {
    let mut ftrs = FuturesUnordered::new();
    
    // Scan this port across all IPs simultaneously
    for ip in &self.ips {
        let socket = SocketAddr::new(*ip, port);
        ftrs.push(self.scan_socket(socket, udp_map.clone()));
    }

    // Process results for current port
    while let Some(result) = ftrs.next().await {
        match result {
            Ok(socket) => open_sockets.push(socket),
            Err(e) => {
            }
        }
    }

    // Apply interval delay before next port
    if self.interval > Duration::from_secs(0) {
        sleep(self.interval).await;
    }
}
```
## Usage
Users can specify the interval using the --interval flag:

`rustscan --interval 2  # Waits 2 seconds between port scans`

- Previous behavior: Scanned ports in parallel batches across all IPs
- New behavior: Scans one port at a time across all IPs, with a configurable delay between ports.
This change provides better control over scan timing while maintaining parallel scanning for individual ports across multiple IPs
