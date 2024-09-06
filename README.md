# Latest Release Version
Action for getting latest (pre-)release's version of a repository, customized property name such as 'created_at' supported.
Updated for GHA's set-output deprecation.
# Usage
```yaml
- name: Get latest release's version(tag_name) of \
    `https://github.com/actions/runner` using action
  id: get-version-action
  uses: fangqiuming/latest-release-version@v1.x
  with:
    repository: actions/runner
    token: ${{ secrets.GITHUB }}
- name: A/B Check
    if: steps.get-version-action.outputs.version != 'v2.289.1'
    uses: actions/github-script@v3
    with:
      script: |
        core.setFailed("${{ steps.get-version-action.outputs.version }} \
        and v2.289.1 are not equivalent!')
```
## Inputs
| Input Name  | Description                                                       | Default Value              |
|-------------|-------------------------------------------------------------------|----------------------------|
| repository  | Repository name with owner. For example, `actions/runner`         | `${{ github.repository }}` |
| token       | [`Personal access token (PAT)`][PAT] used to read the repository  | `${{ github.token }}`      |
| property    | Property name refers to version in [response object][RESPONSE]    | `tag_name`                 |
| include_pre | Should pre-release be included.                                   | `'false'`                  |

[PAT]: https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets
[RESPONSE]: https://docs.github.com/en/rest/reference/releases#get-the-latest-release

## Output
| Output Name | Description                                                                                    |
|-------------|------------------------------------------------------------------------------------------------|
| tag_name    | Tag name of the `repository`'s latest release. For example, `v2.289.1`                         |
| version     | Version value based on preferred `property` name. Output `v0.0.0` if repository has no release |
