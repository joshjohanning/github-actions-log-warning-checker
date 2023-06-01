# github-actions-log-warning-checker

- In a list of repositories, run through recent[^1] workflow runs to see if there are any `set-output` / `save-state` [deprecated workflow command](https://github.blog/changelog/2022-10-11-github-actions-deprecating-save-state-and-set-output-commands/) or [deprecated Node.js 12 actions](https://github.blog/changelog/2022-09-22-github-actions-all-actions-will-begin-running-on-node16-instead-of-node12/) warnings in the logs
- The script outputs the results to a specified CSV file (e.g.: `output.csv`)
- In the output CSV, there is a column to denote whether the warning was found in the latest workflow run or not
- In the output CSV, there is a column to denote which warning it is referencing (deprecated workflow command or deprecated Node.js 12 action)

## Usage

1. Run `gh auth login` to authenticate with GitHub CLI
2. Run `./generate-repos.sh <org> > repos.csv` 
    - Modify list as needed
    - Or create a list of repos in a csv file, `<org/<repo>`, 1 per line, with a trailing empty line at the end of the file
3. Run: `./github-actions-log-warning-checker.sh repos.csv output.csv`

## Example Output

```csv
repo,workflow_name,workflow_url,finding,found_in_latest_workflow_run
joshjohanning-org/actions-linter-testing,CI,https://github.com/joshjohanning-org/actions-linter-testing/blob/main/.github/workflows/blank.yml,Deprecated workflow command,no
joshjohanning-org/actions-linter-testing,new-workflow,https://github.com/joshjohanning-org/actions-linter-testing/blob/main/.github/workflows/new-file.yml,Deprecated workflow command,yes
joshjohanning-org/actions-linter-testing,node12,https://github.com/joshjohanning-org/actions-linter-testing/blob/main/.github/workflows/node12.yml,Node.js 12 action,yes
```

## Sample repos.csv file to use for testing

You can use this `repos.csv` file for testing. It has a finding for a result for a deprecated Node.js 12 action as well as a deprecated workflow command. 

```csv
joshjohanning-org/actions-linter-testing
joshjohanning-org/actions-linter-testing-clean

```

[^1]: Recent is defined as the last 2 workflow runs, modify `WORKFLOW_RUNS_TO_CHECK` as needed.
