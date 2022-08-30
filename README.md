# workflow-sandbox

The following code will make sure that a PR to prod from a branch other than dev will fail. This will only apply if `github.event_name` is `pull_request` (`on: pull_request`).

```
- name: Verify dev PR to prod
  if: ${{ github.base_ref == 'prod' }}
  run: |
    if [[ "$GITHUB_HEAD_REF" != 'dev' ]]
    then
      echo "::error title=Policy violation::Only the dev branch is allowed to PR to the prod branch."
      exit 1
    fi
```
