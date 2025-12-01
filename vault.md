# HashiCorp Vault – Installation & Configuration
Vault is a secrets management and encryption platform.\
\
**Installation (Ubuntu)**
bash
```
sudo apt update
sudo apt install -y vault
```
**Configuration**
1. Configure storage backend and listener (e.g., integrated storage, Consul, etc.) in Vault’s config file.
2. Start Vault in server mode via systemd or directly.
3. Initialize Vault:
bash
```
vault operator init
```
4. Unseal Vault using the generated unseal keys:
bash
```
vault operator unseal
```
(Repeat until unseal threshold is met.)\
5. Authenticate and enable KV secrets engine:
bash
```
vault login
vault secrets enable -path=secret kv
```
6. Define policies and roles, then integrate applications via tokens or dynamic credentials
