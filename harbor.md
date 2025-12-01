# Harbor – Installation & Configuration
Harbor is a cloud-native container registry with security features.\

**Installation**
1. Install Docker and Docker Compose.

2. Download the Harbor installer archive and extract it.

3. Adjust harbor.yml for hostname, ports, and TLS.

4. Run the installer:

bash
```./install.sh```
**Configuration**
Access the Harbor UI and create projects.

Enable vulnerability scanning and configure scanners.

Optionally enable Notary and content signing.

Configure replication rules to other registries if needed.
