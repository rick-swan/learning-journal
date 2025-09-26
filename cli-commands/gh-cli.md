# GitHub CLI (`gh`) Commands Cheat Sheet

## 🔹 Projects
- Install extension
```bash
gh extension install github/gh-projects
```
- List projects for Org
```bash
gh project list --owner Mobilityways --format json --jq '.projects[] | {number,title,url}'
```

## 🔹 Issues

- List open issues assigned to me:
  ```bash
  gh issue list --assignee @me --state open
  ```

- Show issues in JSON format (custom fields):
  ```bash
  gh issue list --assignee @me --state open --json number,title,state,createdAt
  ```

---

## 🔹 Pull Requests

- List open PRs assigned to me:
  ```bash
  gh pr list --assignee @me --state open
  ```

- List open PRs authored by me:
  ```bash
  gh pr list --author @me --state open
  ```

- List PRs where I am requested as a reviewer (via search):
  ```bash
  gh pr list --search "review-requested:@me" --state open
  ```

- View a specific PR (replace `42` with PR number):
  ```bash
  gh pr view 42
  ```

- View a PR in browser:
  ```bash
  gh pr view 42 --web
  ```

---

## 🔹 Reviewing PRs

- Approve a PR:
  ```bash
  gh pr review 42 --approve
  ```

- Comment on a PR:
  ```bash
  gh pr review 42 --comment -b "Looks good!"
  ```

- Request changes on a PR:
  ```bash
  gh pr review 42 --request-changes -b "Please add tests."
  ```

- Approve PR when already on its branch:
  ```bash
  gh pr review --approve
  ```

---

## 🔹 Sprint/Project Management

- List all projects for an organization:
  ```bash
  gh project list --owner mobilityways
  ```

- Get project items with details:
  ```bash
  gh project item-list 1 --owner mobilityways --format json
  ```

- List all open issues assigned to specific user:
  ```bash
  gh issue list --assignee rickswan909 --state open
  ```

- Get issues with custom JSON formatting and priority sorting:
  ```bash
  gh issue list --assignee rickswan909 --state open --json number,title,labels,url --jq 'sort_by(.labels | map(select(.name | startswith("Priority") or startswith("P") or . == "High" or . == "Medium" or . == "Low")) | length) | reverse | .[] | {number, title, priority: (.labels | map(select(.name | startswith("Priority") or startswith("P") or . == "High" or . == "Medium" or . == "Low")) | .[].name // "No Priority"), url}'
  ```

- View detailed issue information:
  ```bash
  gh issue view 5547 --json title,labels,milestone,assignees,state,body
  ```

- Get project views and status options (GraphQL API):
  ```bash
  gh api graphql -f query='query($org: String!, $number: Int!) { organization(login: $org) { projectV2(number: $number) { title views(first: 20) { nodes { id name } } field(name: "Status") { ... on ProjectV2SingleSelectField { options { id name } } } } } }' -f org=mobilityways -F number=1
  ```

- List all sprints/iterations for a project:
  ```bash
  gh api graphql -f query='query($org: String!, $number: Int!) { organization(login: $org) { projectV2(number: $number) { title fields(first: 20) { nodes { ... on ProjectV2Field { id name } ... on ProjectV2IterationField { id name configuration { iterations { startDate title id } completedIterations { startDate title id } } } } } } } }' -f org=mobilityways -F number=6
  ```

- List all projects with details:
  ```bash
  gh project list --owner mobilityways --format json
  ```

- Get project items for specific project:
  ```bash
  gh project item-list 6 --owner mobilityways --format json
  ```

---

## 🔹 Pager / Output Tweaks

- Disable pager temporarily:
  ```bash
  gh issue list | cat
  ```

- Disable pager permanently:
  ```bash
  gh config set pager cat
  ```
