# helm-cleanup-action

Action intended to be called from cleanup bad deploys to do a helm-uninstall.


## Parameters

#### 'namespace' required)
Namespace used by the repo and required for the helm uninstall command.

#### 'aws-access-key-id' (required)
The AWS access key id, should always be for dev.

#### 'aws-secret-access-key' (required)
The AWS secret access key, should always be for dev.

#### 'github-repo' (optional)
The GitHub repository used for optional alerting.

### 'github-run-id' (optional)
The GitHub run id used for optional alerting to show run.

### 'slack-token' (optional)
The Slack token used to authenticate on optional alerting.

### 'destination' (optional)
Destination for messaging, comma separated list. Valid options: committer, #channel-name, email@email.com. Default is #alerts-devops.

## Sample Use

```
helm-cleanup:
  name: "Helm Cleanup"
  runs-on: psidev-linux
  steps:
  - uses: patriotsoftware/helm-cleanup-action@v1
    with:
      namespace: payrollcorepayschedulesapi
      aws-access-key-id: ${{ secrets.DEV_AWS_ACCESS_KEY_ID }}
      aws-secret-access-key: ${{ secrets.DEV_AWS_SECRET_ACCESS_KEY }}    
      slack-token: ${{ secrets.SLACK_TOKEN }}
      destination: "#alerts-devops"
      github-repo: ${{ github.repository }} 
      github-run-id: ${{ github.run_id }}

```
