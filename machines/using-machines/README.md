# Using Machines

## Create a Machine

{% tabs %}
{% tab title="Web UI" %}
The steps below describe how to Create a new Machine via the UI.

Navigate to the Machines page and click "New Machine +" at the top-right:

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.43.52-pm.png)

This will take you to the Machine Create page.

There, select the Region where you want your Machine to reside:

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.40.09-pm.png)

Choose the OS for your Machine:

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.40.23-pm.png)

Toggle whether you want your Machine to bill hourly or monthly, and select your Machine type depending on your desired CPU or GPU:

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.40.34-pm.png)

Select the amount of Storage you want:

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.40.42-pm.png)

You can then specify how many of these Machines you want to create, and type in a name for each of them by clicking the input field that says `New Machine 1` below, for example.

Note that you can also click "Assign Machine" to assign that machine to a particular user on your team, if you are on a team:

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.40.52-pm.png)

Then choose a Network if desired:

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.40.58-pm.png)

Toggle whether you want Auto-Shutdown, Auto Snapshot, and Public IP.

If Auto-Snapshot is enabled, then select the period of time after which auto-shutdown should occur. This is useful, for example, in order to avoid being billed for machine time that you aren't using your Machine but may have forgotten to turn it off.

If Auto Snapshot is enabled, then select the frequency at which you want a snapshot of your Machine to be created and persisted. This is useful in order to ensure that you have a regular backup of your Machine.

If Public IP is enabled, your Machine will be assigned a single static address. This is useful, for example, if you are using your Machine as a persistent server or for a web app.

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.41.04-pm.png)

Finally, click Create Your Paperspace to create your Machine. You will see the amount you'll initially be billed \(for Storage\) as well as the ongoing hourly or monthly cost for the Machine. You can also apply any Promo Code and verify your credit card information before doing so.

![](../../.gitbook/assets/screen-shot-2019-07-11-at-6.43.02-pm.png)

Et voilà! Your Machine will spin up in the background, and you'll see it appear back on the Machines list page.
{% endtab %}

{% tab title="CLI" %}
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
      <td style="text-align:left">The script id of a script to be run on startup. See <a href="https://github.com/Paperspace/paperspace-node/blob/master/scripts.md">the Script Guide</a> for
        more info on using scripts</td>
    </tr>
  </tbody>
</table>
{% endtab %}
{% endtabs %}

