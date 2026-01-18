 Debugging Container Connectivity
 
**Scenario:** A containerized app cannot reach a database running on the same host.

1. Investigation Steps
* Verify Mapping: `docker ps` to ensure host ports are mapped correctly (e.g., `8080:80`).
* Check Network: `docker network inspect bridge` to see if both containers are on the same network.
* Inspect Container: `docker exec -it [id] ping [db_container_name]`.

2. Common Solutions
* DNS Resolution: Use Docker's built-in DNS by using container names instead of IP addresses.
* Port Conflict: Ensure no other service on the Mac/Server is using the same host port.
