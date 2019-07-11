# List Machines

**Usage:** 

`gradient machines list [OPTIONS]`

List information about all machines available to either the current authenticated user or the team, if the user belongs to a team. The list method takes an optional first argument to limit the returned machine objects.

**Options:**

`--params JSON_STRING` ****JSON used to filter machines. Use either ****this or a combination of following options

`--machineId TEXT`Optional machine id to match on

`--name TEXT` Filter by machine name

`--os TEXT`Filter by os used

`--ram INTEGER` Filter by machine RAM \(in bytes\)

`--cpus INTEGER` Filter by CPU count

`--gpu TEXT` Filter by GPU type

`--storageTotal TEXT` Filter by total storage

`--storageUsed TEXT` Filter by storage used

`--usageRate TEXT` Filter by usage rate

`--shutdownTimeoutInHours INTEGER`Filter by shutdown timeout

`--performAutoSnapshot BOOLEAN` Filter by performAutoSnapshot flag

`--autoSnapshotFrequency [hour|day|week]` Filter by autoSnapshotFrequency flag

`--autoSnapshotSaveCount INTEGER` Filter by auto shapshots count

`--agentType TEXT` Filter by agent type

`--dtCreated TEXT` Filter by date created

`--state TEXT` Filter by state

`--updatesPending TEXT`Filter by updatesPending

`--networkId TEXT` Filter by network ID

`--privateIpAddress TEXT`Filter by private IP address

`--publicIpAddress TEXT`Filter by public IP address

`--region [CA1|NY2|AMS1]`Filter by region

`--userId TEXT`Filter by user ID

`--teamId TEXT`Filter by team ID

`--dtLastRun TEXT`Filter by last run date

`--apiKey TEXT`API key to use this time only

`--help` Show help message.

