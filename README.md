# haproxy-load-balancing-simulation

**Description:**
A comprehensive load balancing simulation project built with **Java**, **HAProxy**, and **Docker Compose**.
This project demonstrates HTTP and TCP load balancing, health checks, and advanced failover behaviors using multiple backend services and a backup server.
You can easily observe how HAProxy distributes traffic, handles server failures, and automatically routes requests to backup infrastructure, all within an isolated container environment.

## Key Features:

* Supports both **Layer 4 (TCP)** and **Layer 7 (HTTP)** load balancing with separate HAProxy configurations
* Path-based routing and per-endpoint failover logic for HTTP requests (Layer 7)
* Transparent round robin balancing and failover for generic TCP traffic (Layer 4)
* Automatic backup server activation in case of backend failures
---

**How to Build and Run:**

```bash
docker compose up --build
```

All components will be built and started automatically. This includes:

* Three main Java backend servers and a dedicated backup server
* HAProxy in both Layer 4 (TCP) and Layer 7 (HTTP) proxy modes
* Pre-configured routing and health check scenarios

---

**How to Simulate Failover and Load Balancing:**

* **Test HTTP Layer 7:**
  Send requests to [http://localhost:8087/](http://localhost:8087/) with different endpoints (e.g., `/api/hello`, `/auth/hello`, `/other/hello`, `/`)
  Observe how traffic is routed according to endpoint and how backup takes over if a primary server fails.

* **Test TCP Layer 4:**
  Send requests to [http://localhost:8084/](http://localhost:8084/) and see round robin balancing among healthy servers.
  When all primary servers are down, backup-server automatically handles all traffic.

* **Simulate Failover:**
  While the system is running, stop any backend server using:

  ```bash
  docker stop server2
  ```

  or

  ```bash
  docker stop server1
  ```

  Watch as HAProxy reroutes traffic to the remaining healthy servers or backup according to your configuration.

* **Logs and Troubleshooting:**
  All HAProxy and backend logs can be viewed using:

  ```bash
  docker logs <container_name>
  ```

---

