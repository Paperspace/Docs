# Node Attributes

Each gradient-node instance has a set of environment related attributes, such as cpu\_count and gpu\_model, which can be used in the `nodeAttrs` scheduling option at job creation in order to select a compatible gradient-node instance for the job.  For example this option would select a machine with 4 cpus:

    `--nodeAttrs '{"cpu_count":2}'`

One or more attribute values can be combined by expressing them as attributes of a valid JSON object string. Each of the attribute names must be enclosed in double quotes, as should any string attribute values, e.g:

    `"gpuModel":"Nvidia GTX 1080 Ti"`

{% hint style="info" %}
Numeric and true/false values do not need to be double quoted.
{% endhint %}

Each attribute name and its corresponding value must be separated by a colon.  Multiple attribute-value pairs are separated by a comma. The list of attribute-value pairs are then enclosed in curly braces to complete the JSON object string.

If there are any spaces in the quoted string values, or or anywhere else in the JSON object string, then the entire string should be enclosed in single quotes.  Here is a complete example:

   `--nodeAttrs '{"gpuModel":"Nvidia GTX 1080 Ti", "cpuCount":2}'`

You can determine the node attributes of a given gradient-node instance by checking the node details in the cluster view within your account, or by examining the console output of the gradient-node instance upon startup.  


Here is the current list of supported node attributes, and their types:

| Attribute | Type |
| :--- | :--- |
| "cpuCount" | number |
| "cpuHostname" | string |
| "cpuMem" | string |
| "cpuModel" | string |
| "gpuCount" | string |
| "gpuDevice" | string |
| "gpuDriver" | string |
| "gpuMem" | string |
| "gpuModel" | string |
| "gpuSerial" | string |
| "gradientNodeVersion" | string |



