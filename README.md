# github-actions-log-warning-checker

- Runs through recent[^1] workflow runs to see if there are any warnings in the logs
- Outputs results to a specified CSV file
- In the output CSV, there is a column to denote whether the warning was found in the latest workflow run or not

## Usage

1. Run `gh auth login` to authenticate with GitHub CLI
2. Run `./generate-repos.sh <org> > repos.csv` 
    - Modify list as needed
    - Or create a list of repos in a csv file, `<org/<repo>`, 1 per line, with a trailing empty line at the end of the file
3. Run: `./github-actions-log-warning-checker.sh repos.csv output.csv`

## Example Output

```csv
repo,workflow_name,workflow_url,found_in_latest_workflow_run
joshjohanning-org/actions-linter-testing,CI,https://github.com/joshjohanning-org/actions-linter-testing/blob/main/.github/workflows/blank.yml,no
joshjohanning-org/actions-linter-testing,new-workflow,https://github.com/joshjohanning-org/actions-linter-testing/blob/main/.github/workflows/new-file.yml,yes
```

[^1]: Recent is defined as the last 5 workflow runs, modify `WORKFLOW_RUNS_TO_CHECK` as needed.
