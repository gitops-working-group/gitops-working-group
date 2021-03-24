# Contributing

This document <https://github.com/gitops-working-group/gitops-working-group/blob/main/CONTRIBUTING.md> defines the contribution process for the GitOps Working Group project and community.
These guidelines apply to all git repositories in the `gitops-working-group` GitHub org, however each repository may specify additional contribution processes.

## Getting Involved

With the announcement of the GitOps Working Group the founders would like to invite other companies to join the group and contribute to the community and the adoption of GitOps across the cloud native landscape.
There are a few ways you can get involved:

- Watch or star this repo to see when things change.
- Attend a [Working Group meeting](./MEETINGS.md).
- Join `#wg-gitops` on [CNCF Slack](https://slack.cncf.io/) and share how you're using GitOps and any important considerations we should include.

We'll review all open issues and PRs at our regular working group meeting (schedule coming soon).

### Pull Request Tips - Submitting and Reviewing

- Talk to us via GitHub issue, mailing list, or meeting before you start on major
work. If it’s typos and fixes to docs, please submit. 😀
- When making changes to your PR, put them into a new commit (instead of rebasing
  or amending) so that it's easier for reviewers to see just your new changes.
- We will give you an opportunity to clean up your commits before merging or can
squash them for you.
- If a member asks you to "rebase" your PR, they're saying that a lot of docs/code
 has changed, and that you need to update your branch to incorporate the latest
 changes from main before we can merge your PR. You can use whatever you are
 comfortable with, either merging main into your branch or rebasing your
 branch on main.

## Certificate of Origin

Developer Certificate of Origin (DCO) commit signoff is required for all new code contributions.
This is automatically checked by the [Probot: DCO](https://github.com/probot/dco/) integration across all `gitops-working-group` GitHub org repositories.

Commit signoff is a simple statement that you, as a contributor, have the legal right to make the contribution.
See `git help commit`:

> The meaning of a signoff depends on the project, but it typically certifies that committer has the rights to submit this work under the same license and agrees to a Developer Certificate of Origin (see <http://developercertificate.org/> for more information).

### CLI

When signing commits with `git commit -s`, signoff is drawn automatically from your `user.name` and `user.email` git configs.
If you choose to manually add a signoff line to your commit message, it must be properly formatted and match your commit information. For example, when using the GitHub [private email option](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-user-account/setting-your-commit-email-address) you must set your git config email accordingly.
For those who wish to ensure this is always done in your CLI, consider implementing something like [this gist](https://gist.github.com/scottrigby/0c043c0bfbbdb5949e2d824fc3adeaa4).

### Browser

For contributions made with the GitHub UI — including [applying suggested changes](https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/incorporating-feedback-in-your-pull-request) — the [scottrigby/dco-gh-ui](https://github.com/scottrigby/dco-gh-ui) browser extension is recommended.
This pre-fills GitHub's commit textareas with a properly formatted signoff from your configured name and email.
Otherwise, you will need to be sure to do so manually.
