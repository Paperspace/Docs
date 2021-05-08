# Storing an API key as a Secret

Certain actions within Gradient require incorporating your API key to authenticate requests.  In cases where your API key is used within your code or commands that may be visible within your Gradient team \(e.g. a Notebook\) or other locations \(e.g. when checking your code into source control\), you will want to use Secrets to mask your unique API key.  

### 1. Create a new API key

![Creating a new API key from the team settings page](../../.gitbook/assets/screen-shot-2021-05-08-at-2.49.26-pm.png)

Once your key is created, copy the key to your clipboard.

### 2. Save the key as a Secret

Add a name, paste the API key in the Value field, and click Add. 

![Creating a Secret](../../.gitbook/assets/screen-shot-2021-05-08-at-2.51.34-pm.png)

