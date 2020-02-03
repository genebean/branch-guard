# Block PR merges when Checks for target branches are failing

Create following `.github/workflows/branch-guard.yml` that will block PRs from merging when the latest [Check Suite](https://developer.github.com/v3/checks/)
starts failing and unblock once it's passing again:

```yaml
on:
  check_suite: # to update all PRs upon a Check Suite completion
    type: ['completed']
    branches:
      - master # branches to guard
  pull_request: # to update newly open PRs
    type: ['opened']
  
name: Branch Guard
jobs:
  branch-guard:
    name: Branch Guard
    runs-on: ubuntu-latest
    steps:
    - uses: cirrus-actions/branch-guard@v1
      with:
        appsToCheck: Cirrus CI # or any other App name (can be a comma separated list of names)
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
