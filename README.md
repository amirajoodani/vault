***

# 🔐 HashiCorp Vault Cheat Sheet

## 🔑 Authentication (Auth Methods)
| Command | Description |
| :--- | :--- |
| `vault auth list` | List all enabled authentication methods |
| `vault auth enable <method>` | Enable a new auth method (e.g., `userpass`, `approle`, `oidc`) |
| `vault write auth/<method>/role/<name> ...` | Create or update a specific role |
| `vault read auth/<method>/role/<name>` | Read details of a specific role |
| `vault login -method=<method> [options]` | Log in using a specific method |

## 🎫 Tokens
| Command | Description |
| :--- | :--- |
| `vault token create [options]` | Create a new token |
| `vault login <token>` | Log in using a provided token |
| `vault token lookup` | Lookup details of your current token |
| `vault token lookup <token>` | Lookup details of a specific token |
| `vault token revoke <token>` | Revoke a specific token |

## ⚙️ Secrets Engines
| Command | Description |
| :--- | :--- |
| `vault secrets list` | List all enabled secrets engines |
| `vault secrets list --detailed` | List detailed information about engines |
| `vault secrets enable <type>` | Enable a new secrets engine |
| `vault secrets enable -path=<path> <type>` | Enable engine at a custom path |
| `vault secrets disable <path>` | Disable a secrets engine at the given path |

## 📜 Policies (ACL)
| Command | Description |
| :--- | :--- |
| `vault policy list` | List all existing policies |
| `vault policy write <name> <file.hcl>` | Create/update policy from an HCL file |
| `vault policy write <name> -<<EOF ... EOF` | Create policy using inline HCL (Heredoc) |
| `vault policy read <name>` | View the contents of a policy |
| `vault policy delete <name>` | Delete a policy |

## 🛠️ Day-to-Day Operations & Cluster
| Command | Description |
| :--- | :--- |
| `vault status` | Check Vault status (Seal, HA, etc.) |
| `vault operator unseal` | Unseal Vault using a key shard |
| `vault operator members` | List all nodes in the cluster (Raft/HA) |
| `vault operator raft list-peers` | List Raft cluster peers |
| `vault operator raft snapshot save <file>`| Save a snapshot of Vault data |
| `vault operator step-down` | Force active node to give up leadership |

## 🔄 Replication (Enterprise Feature)
| Command | Description |
| :--- | :--- |
| `vault read sys/replication/status` | Check current replication status |
| `vault write -f sys/replication/dr/primary/enable` | Enable DR replication on primary cluster |
| `vault write sys/replication/dr/primary/secondary-token id=<name>` | Generate token for DR Secondary cluster |
| `vault write sys/replication/dr/secondary/enable token=<token>` | Enable node as DR Secondary |

## 📦 KV Secrets (Key-Value)
*Note: `undelete` and `metadata delete` require **KV-V2***

| Command | Description |
| :--- | :--- |
| `vault kv put secret/myapp key=value` | Store a new secret |
| `vault kv get secret/myapp` | Read/Retrieve a secret |
| `vault kv delete secret/myapp` | Delete a secret |
| `vault kv undelete -versions=1 secret/myapp` | Restore a deleted version (**KV-V2**) |
| `vault kv metadata delete secret/myapp` | Permanently remove metadata & versions (**KV-V2**) |

***
