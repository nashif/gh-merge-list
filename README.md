# gh merge-list

A [GitHub CLI](https://cli.github.com) extension that shows the Zephyr
[merge list](https://merge-list.zephyrproject.io) in the terminal and lets you
merge the pull requests that are ready.

## Install

    gh extension install nashif/gh-merge-list

Requires Python 3.8+. Uses [fzf](https://github.com/junegunn/fzf) for the
interactive picker when available.

## Usage

    gh merge-list                       # ready PRs, all targets
    gh merge-list list -s all           # everything on the list
    gh merge-list list -t v4.4-branch   # ready PRs for one target
    gh merge-list list --mine           # ready PRs assigned to me
    gh merge-list list --json           # machine-readable output
    gh merge-list show 116871           # details for one or more PRs

    gh merge-list merge 116871 116863   # merge specific PRs (confirmation prompt)
    gh merge-list merge --all -t main   # merge every ready PR targeting main
    gh merge-list merge ... -n          # dry run
    gh merge-list pick                  # choose PRs interactively, then merge

Merges go through `gh pr merge --rebase` (change with `--method`). PRs whose
merge gates are not all green are never merged, even if named explicitly.

The merge list is a periodic snapshot, so every PR is re-checked live on
GitHub before the confirmation prompt and again immediately before its own
merge, and is skipped if it is no longer open, is a draft,
has merge conflicts, has changes requested by a reviewer, or has failing or
still-running CI.
