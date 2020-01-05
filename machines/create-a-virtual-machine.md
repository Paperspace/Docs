---
description: Create a new Paperspace virtual machine
---

# Create a Machine via the CLI

This page and the subsequent pages in this section document how to use the CLI to operate on Paperspace Machines.

**Usage:** 

```bash
gradient machines create [OPTIONS]
```

Create a new Paperspace virtual machine. If you are using an individual account, you will be assigned as the owner of the machine. If you are a team administrator, you must specify the user that should be assigned to the machine, either by specifying a user id, or by providing an email address, password, first name and last name for the creation of a new user on the team.

**Parameters:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>region [CA1|NY2|AMS1]</code>
      </td>
      <td style="text-align:left">Name of the region (required)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>machineType [Air|Standard|Pro|Advanced|GPU+|P4000|P5000|</code>
        </p>
        <p><code>P6000|V100|C1|C2|C3|C4|C5|C6|C7|C8|C9|C10]</code>
        </p>
      </td>
      <td style="text-align:left">Machine type (required), pick one</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>size (INTEGER)</code>
      </td>
      <td style="text-align:left">Storage size for the machine in GB (required)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>billingType [monthly|hourly]</code>
      </td>
      <td style="text-align:left">Either monthly or hourly billing (required)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>machineName</code>
      </td>
      <td style="text-align:left">A name for this machine (required)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>templateId</code>
      </td>
      <td style="text-align:left">Template id of the template to use for creating this machine (required)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>assignPublicIp</code>
      </td>
      <td style="text-align:left">Assign a new public ip address on machine creation. Cannot be used with <code>dynamicPublicIp</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>dynamicPublicIp</code>
      </td>
      <td style="text-align:left">Assigns a new public ip address on machine start and releases it from
        the account on machine stop. Cannot be used with <code>assignPublicIp</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>networkId (TEXT)</code>
      </td>
      <td style="text-align:left">If creating on a specific network, specify its id</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>teamId (TEXT)</code>
      </td>
      <td style="text-align:left">If creating the machine for a team, specify the team id</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>userId (TEXT)</code>
      </td>
      <td style="text-align:left">If assigning to an existing user other than yourself, specify the user
        id (mutually exclusive with email, password, firstName, lastName)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>email (TEXT)</code>
      </td>
      <td style="text-align:left">If creating a new user for this machine, specify their email address (mutually
        exclusive with userId)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>password (TEXT)</code>
      </td>
      <td style="text-align:left">If creating a new user, specify their password (mutually exclusive with
        userId)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>firstName (TEXT)</code>
      </td>
      <td style="text-align:left">If creating a new user, specify their first name (mutually exclusive with
        userId)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>lastName (TEXT)</code>
      </td>
      <td style="text-align:left">If creating a new user, specify their last name (mutually exclusive with
        userId)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>notificationEmail (TEXT)</code>
      </td>
      <td style="text-align:left">Send a notification to this email address when complete</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>scriptId (TEXT)</code>
      </td>
      <td style="text-align:left">The script id of a script to be run on startup. See the Script Guide for
        more info on using scripts</td>
    </tr>
  </tbody>
</table>