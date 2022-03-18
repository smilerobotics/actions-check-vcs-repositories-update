# check-vcs-repositories-update

## Description

An action to check repositories update defined in vcs config.

## Required input

1. vcs_setting_file: Path of the file for vcs import.
1. working_directory: Working directory.
1. command_output: Path of the vcs export output file.
1. cache_key_prefix: Key prefix for cache of the vcs export output file.

## Output

1. is_updated: If the repository is updated, true.

## Example

```yaml
jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - run: |
          echo "repositories:" >/tmp/vcs.repos
          echo "  actions-check-vcs-repositories-update:" >>/tmp/vcs.repos
          echo "    type: git" >>/tmp/vcs.repos
          echo "    url: https://github.com/smilerobotics/actions-check-vcs-repositories-update" >>/tmp/vcs.repos
          echo "    version: main" >>/tmp/vcs.repos
          echo "  actions-check-github-repository-update:" >>/tmp/vcs.repos
          echo "    type: git" >>/tmp/vcs.repos
          echo "    url: https://github.com/smilerobotics/actions-check-github-repository-update" >>/tmp/vcs.repos
          echo "    version: main" >>/tmp/vcs.repos
        shell: bash
      - uses: smilerobotics/actions-check-vcs-repositories-update@v1
        id: check
        with:
          vcs_setting_file: /tmp/vcs.repos
          working_directory: .
          command_output: ~/is_updated
          cache_key_prefix: "is-updated"
      - run: echo ${{ steps.check.outputs.is_updated }}
        shell: bash
```
