# Destroy a Machine

**Usage:**

`gradient machines destroy [OPTIONS]`

Destroy the machine with the given id. When this action is performed, the machine is immediately shut down and marked for deletion from the datacenter. Any snapshots that were derived from the machine are also deleted. Access to the machine is terminated immediately and billing for the machine is prorated to the hour. This action can only be performed by the user who owns the machine, or in the case of a team, the team administrator.

####  Parameters**:**

| `Name` | Description |
| :--- | :--- |
| `--machineId TEXT` | Id of the machine to destroy \(required\) |
| `--releasePublicIp  BOOL` | Releases any assigned public ip address for the machine; ****defaults to false |

