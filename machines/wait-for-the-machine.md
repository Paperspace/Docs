# Wait For a Machine

**Usage:** 

`gradient machines waitfor [OPTIONS]`

Wait for the machine with the given id to enter a certain machine state. This action polls the server and returns only when we detect that the machine has transitioned into the given state.

**Options:**

`--machineId TEXT` Id of the machine to start  \[required\]

`--state [off|serviceready|ready]` Name of the state to wait for  \[required\]

`--apiKey TEXT` API key to use this time only

`--help` Show help message

