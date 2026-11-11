# ProtoBot-template

This repository is a GitHub template for starting ProtoBot-based projects.
GitHub template repositories copy files but not repository settings, so each new project must apply the settings below.

## Post-instantiation setup checklist

| Setting | Location | Value |
|---|---|---|
| Merge method | Settings > General > Pull requests | Enable squash merge. Disable merge commits and rebase merging. |
| Squash message sources | Settings > General > Pull requests | Set the squash commit title to the pull request title. Set the squash commit message to the pull request body. The non-closing check validates those two fields, so the merged text must come from them. |
| Linked pull request auto-close | Settings > General > Issues | Disable Auto-close issues with merged linked pull requests. The coordinator owns closure. A merge must not close a source issue or a managed implementation issue. |
| Branch ruleset | Settings > Rules | Require one approving review, require status checks to pass, block force pushes, and block deletion. The required status check is the single aggregate gate job. Specify `<aggregate-gate-job>` as a placeholder that the project fills in. |
| Labels | Issues > Labels | Create `assignment-active`, `ready-to-code`, `needs-replan`, `superseded`, and `queued`. The `assignment-active` label holds the requirement scope, and `ready-to-code` is the dispatch signal. |
| Actions variables and secrets | Settings > Secrets and variables > Actions | Set `FULLSEND_MINT_URL`, `FULLSEND_GCP_REGION`, and `FULLSEND_PROJECT_NUMBER` as variables. Set `FULLSEND_GCP_WIF_PROVIDER`, `FULLSEND_GCP_PROJECT_ID`, and the model credential secret. The exact names must match the pinned upstream workflow. |
| Automatic triage | `.fullsend/harness/triage.yaml` | Keep `TRIAGE_AUTO_CODE` off. Human intake and drafting own source issues. |
| Coordinator status issue | Issues, and Settings > Secrets and variables > Actions > Variables | Create one stable issue. Store its number in a repository variable. It must not receive `ready-to-code`, `assignment-active`, triage, backlog, or closure treatment. |
| Coordinator caller | `.github/workflows/` | Install the repository-owned caller workflow through a human-authenticated pull request. Agent tokens cannot write workflow files. |
| Specification | Root directory and `spec/requirements/` | Replace the empty `Vision.md` and `Architecture.md` with the project's own content. Add the first requirement records under `spec/requirements/`. |

### Verify the setup

1. Open a pull request that references an issue without a closing keyword.
2. Merge it with squash.
3. Confirm the linked issue stays open.
4. Confirm the squash commit message equals the pull request title and body.
