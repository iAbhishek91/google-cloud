# Cloud load-balancing

Load balancer are managed by google. so don't worry about scaling or managing them.

**when we VM auto scaling, how does customer reaches the application** - using cloud VMs.

Supports both TCP, UDP traffic, as well as HTTP/HTTPs.

One IP can direct traffic to any region around the world, supports cross region load balancing.

Also includes multi region failover.

They are very responsive to health of the application, failover etc.

LB do not require pre-warming as they are not hardware load balancer.

## Type of load balancing

- **Global HTTPS Load balancing**:
  - Layer 7(application layer) load balancing. (HTTP(s))
  - Anycast IP address
  - supports HTTP  (80 or 8080) and HTTP(s) 443
  - supports both IPV4 and IPv6
  - supports QUIC protocol: which is a LAYER-4 protocol used for faster client connection.
  - autoscaling
  - HTTPs SSL session terminates at the load balancer.
  - *Forwarding rule*: forwards the packets to HTTP proxy *or in case of HTTPs to a HTTPs proxy.
  - *target HTTP(s) proxy*: this proxy server checks the URL map and forwards the packet to appropriate backend service load balancer.
    - in case of HTTPs, at least one signed certificate is required. Up to 10 certificates are supported.
    - **SSL certificate is also a resource**. SSL certificate keeps the certificate information. *This resource are used only with load balancers proxies such as HTTPs proxy and SSL proxy*.
  - *URL maps*: to route based on URLs to other set of instances.
  - *Backend service*: forwards the traffic to to the backend based on the location, and resource utilization etc.
  - *Backend* (refer the image NW-02b-cloud-HTTPS-LB.png)
    - health check to be configured
    - does round robin, but can this rule can be overridden using session affinity.
    - defaults timeout after 30 seconds.
    - contains:
      - an instance group: *managed or unmanaged, with or without auto-scaling*
      - a balancing mode: inform the load balancer that the instance is at fullest. *This can be CPU utilization or request per sec(RPS). This parameter cant be used for auto-scaling*
      - a capacity scaler: additional control that interact with balancing mode. *for operating at max of 80% CPU utilization, configure BM as 80% and capacity scaler with 100%, if you want to cut instance utilization into half the set BM to 80% and capacity scaler with 50%.*
    - any change to the network are NOT instantaneous and it takes minutes to propagate the change over the network.
  - health check recommended for load balancing scenario.
- **Global SSL Proxy**:
  - Layer 4 load balancing of non HTTPs SSL traffic based on load.
  - Supported on specific port number.
  - Terminates TLS session at load balancing layer and forwards the traffic to instance using TCP or TLS/SSL protocol. *SSL lb also forwards traffic based on the nearest instance and healthy instance available using TCP or SSL*.
  - supports IPV4 and IPV6
  - Supports:
    - intelligent routing: understand capacity of the backends, health check and also location.
    - certificate management: only need to upload customer facing certificate. rest all is taken care by google.
    - auto security patching of the load balancer, when required
    - SSL policies.
- **Global TCP Proxy**:
  - Exactly same as SSL proxy load balancer, only difference it do not perform any certificate management.
- **Regional/ network load balancing**:
  - Load balancing of any traffic (TCP and UDP). Supports any port number.
  - non proxy load balancer unlike Glocal SSL proxy & TCP proxy load balancer.
  - *Backend*:
    - can be *instance group*:
    - or *target pool*: they are resource that defines a group of instance that receive incoming traffic from forwarding rules.
      - the destination instance is picked by the load balancer based on the HASH of source IP:port and destination IP:port.
      - supports only TCP and UDP
      - should be in the same region
      - Each target pool can have only one health check
      - 50 target pool per project is possible.
  - it uses *maglev*, large  distributed software system.
- **Regional internal TCP**:
  - Load balancing of traffic inside VPC.
  - Use for the internal tiers of multi-tier application.
  - Layer-4(TCP/UDP).
  - Layer-4 uses *Andromeda*, which is google software defined network virtualization stack. *Generally in proxy based load balancer like TCP proxy load balancer or SSL proxy load balancer there is two connection created. One b/w client and load balancer and load balancer to the instances. However regional load balancer do for creat two connection. The client directly connects with the instance load balancer only help in between. This is possible because of Andromeda's network virtualization stack.*
  - use case: traditional 3 tier application.
- **Regional internal Http(s)**:
  - and Layer-7(HTTP(s))-BETA load balancers
  - Layer-7 is a proxy based load balancer

## Decision tree points

- Use **global HTTPs|SSL proxy|TCP proxy load balancer**
  - when user is distributed globally.
  - access application across the globe using the same IP address.
  - IPV6 is supported, *act as a reverse proxy which terminate the IPv6 connection, and initiate a IPv4 connection to the internal network, and vice-versa while sending response*.
- **Regional internal TCP**:
  - we can run and scale application behind a internal IP address.
  - accessible in load balancers region in same VPC.
  - IPV6 is not supported
  - RFC 1918 only
