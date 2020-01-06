# Start a Machine

**Usage:**

```text
gradient machines start [OPTIONS]
```

Start up an individual machine. If the machine is already started, this action is a no-op. If the machine is off, it will be booted up. This action can only be performed by the user who owns the machine.

**Parameters:**

| Name | Description |
| :--- | :--- |
| `machineId (TEXT)` | Id of the machine to start \(required\) |

