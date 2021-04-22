# Code

Notebooks, Workflows, and Deployments include source code integrations to connect and track your code.  

{% hint style="info" %}
GradientCI is **not** yet supported in Workflows — [stay tuned](https://updates.paperspace.com/) for updates.  This feature is scheduled to be released in Q2 2021.
{% endhint %}

[GradientCI](https://gradient.paperspace.com/gradientci) is our current implementation of source control integration which supports both tracking commits \(or branches\) as well as optionally feeding Gradient model performance metrics back into GitHub.  This tool is supported in a enterprise version of Gradient which is being deprecated in favor of [Workflows](../explore-train-deploy/workflows-1/).  Workflows support pulling your code as a Gradient action called `git-checkout` which you can learn about [here](../explore-train-deploy/workflows-1/gradient-actions.md#git-checkout).

**Git tracking in GradientCI**

![](../.gitbook/assets/image%20%2854%29.png)

**Inline Git diffing**

![](../.gitbook/assets/image%20%2840%29.png)

**GitHub Pull Request integration with commenting & status checks**

![](../.gitbook/assets/image%20%2842%29.png)



