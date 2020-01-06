# Stop a Machine

**Usage:** 

```text
gradient machines stop [OPTIONS]
```

Stop an individual machine. If the machine is already stopped or has been shut down, this action is a no-op. If the machine is running, it will be stopped and any users logged in will be immediately kicked out. This action can only be performed by the user who owns the machine.

**Parameters:**

| Name | Description |
| :--- | :--- |
| `machineId (TEXT)` | Id of the machine to start \(required\) |

