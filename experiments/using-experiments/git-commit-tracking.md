# Git Commit Tracking

If you are using [GradientCI](../../projects/gradientci-v2/), the specific code commit used in an Experiment will automatically be tracked for you.  If you are not using GradientCI, however, you can tag a commit manually so your Experiments are associated with your code.  This is accomplished using the `--workspaceRef` command.  

### Example

```bash
gradient experiments run ... --workspaceRef 68ace0d9881a968e6470accbff60a6d6728f69d1
```

The commit is now tracked as an Experiment parameter:

![](../../.gitbook/assets/image%20%2854%29.png)

