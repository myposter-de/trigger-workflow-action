# Trigger Workflow and Wait

Github Action for trigger a workflow from another workflow.

**When would you use it?**

When deploying an app you may need to deploy additional services, this Github Action helps with that.


## Arguments

| Argument Name            | Required   | Default     | Description           |
| ---------------------    | ---------- | ----------- | --------------------- |
| `owner`                  | True       | N/A         | The owner of the repository where the workflow is contained. |
| `repo`                   | True       | N/A         | The repository where the workflow is contained. |
| `github_token`           | True       | N/A         | The Github access token with access to the repository. Its recommended you put it under secrets. |
| `workflow_file_name`     | True       | N/A         | The reference point. For example, you could use main.yml. |
| `ref`                    | False      | main        | The reference of the workflow run. The reference can be a branch, tag, or a commit SHA. |
| `client_payload`         | False      | `{}`        | Payload to pass to the workflow, must be a JSON string |


## Example

```yaml
- name: Checkout Action
  uses: actions/checkout@v3
  with:
    repository: myposter-de/trigger-workflow-action
    ref: refs/heads/master
    path: ./.github/actions/trigger-workflow
    token: ${{ secrets.DEVOPS_USER_TOKEN }}
          
- uses: myposter-de/trigger-workflow-action
  with:
    github_token: ${{ secrets.DEVOPS_USER_TOKEN }}
    owner: myposter-de
    repo: myrepo
    ref: master
    workflow_file_name: deployment.yaml
    client_payload: '{
          "application": "",
          "reference_branch": "",
          "helm_chart_version": ""
        }'
```

## Testing

You can test out the action locally by cloning the repository to your computer. You can run:

```shell
INPUT_GITHUB_TOKEN="<REDACTED>" \
INPUT_OWNER="me" \
INPUT_REPO="myrepo" \
INPUT_REF="release-branch" \
INPUT_WORKFLOW_FILE_NAME="main.yml" \
INPUT_CLIENT_PAYLOAD='{}' \
entrypoint.sh
```
