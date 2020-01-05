# Wait For a Machine

**Usage:** 

```text
gradient machines waitfor [OPTIONS]
```

Wait for the machine with the given id to enter a certain machine state. This action polls the server and returns only when we detect that the machine has transitioned into the given state.

**Parameters:**

| Name | Description |
| :--- | :--- |
| `machineId (TEXT)` | Id of the machine to start \(required\) |
| `state [off|serviceready|ready]` | Name of the state to wait for \(required\) |

