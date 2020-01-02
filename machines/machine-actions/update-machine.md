# Update a Machine

**Usage:** 

`gradient machines update [OPTIONS]`

Update attributes of a machine.

**Parameters:**

| Name | Description |
| :--- | :--- |
| `machineId (TEXT)` | Id of the machine to start \(required\) |
| `machineName (TEXT)` | New name for the machine |
| `shutdownTimeoutInHours (INTEGER)` | Number of hours before machine is shutdown if no one is logged in via the Paperspace client |
| `shutdownTimeoutForces (BOOLEAN)` | Force shutdown at shutdown timeout, even if there is a Paperspace client connection |
| `performAutoSnapshot (BOOLEAN)` | Perform auto snapshots |
| `autoSnapshotFrequency [hour|day|week|null]` | Frequency at which to automatically create a snapshot of the machine |
| `autoSnapshotSaveCount (INTEGER)` | Number of snapshots to save |
| `dynamicPublicIp (BOOLEAN)` | If true, assigns a new public ip address on machine start and releases it from the account on machine stop |

