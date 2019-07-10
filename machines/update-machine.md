# Update machine

**Usage:** 

`gradient machines update [OPTIONS]`

Update attributes of a machine

**Options:**

  `--machineId TEXT`  Id of the machine to update  \[required\]

  `--machineName TEXT` New name for the machine

  `--shutdownTimeoutInHours INTEGER` Number of hours before machine is shutdown if no one is logged in via the Paperspace client

  `--shutdownTimeoutForces BOOLEAN` Force shutdown at shutdown timeout, even if there is a Paperspace client connection

  `--performAutoSnapshot BOOLEAN`   Perform auto snapshots

  `--autoSnapshotFrequency [hour|day|week]` One of 'hour', 'day', 'week', or null

  `--autoSnapshotSaveCount INTEGER` Number of snapshots to save

  `--dynamicPublicIp BOOLEAN` If true, assigns a new public ip address on machine start and releases it from the account on machine stop

  `--apiKey TEXT` API key to use this time only

  `--help` Show help message.

