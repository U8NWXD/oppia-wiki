## Table of contents

* [PR lifecycle](#pr-lifecycle)
* [Draft pull requests](#draft-pull-requests)
* [Labeling issues and pull requests](#labeling-issues-and-pull-requests)
* [Juggling multiple pull requests](#juggling-multiple-pull-requests)

## PR lifecycle

![Flowchart of PR lifecycle](images/prLifecycle.png)

<details>
<summary>Flowchart source code</summary>

The flowchart was generated from the below source code by https://flowchart.fun.

```text
~~~
layout:
  name: dagre
  rankDir: LR
~~~
Draft PR
  Ready for review: PR awaiting review
    Request changes: Changes requested
      Addresses comments: (PR awaiting review)
    All reviewers approve: PR labeled LGTM
      Merge: PR closed
```
</details>

1. (optional) Draft PR: Authors can open draft PRs to get early feedback or debug CI tests. Reviews at this stage are at the discretion of the author.
2. PR ready for review: Once authors mark PRs as ready for review (or if they skip the draft PR stage entirely), reviews will automatically be requested from all code owners. Oppiabot will assign one developer (typically the developer from the changelog label) to take a first pass. Oppiabot will assign the other code owners to review once the first pass is complete.
3. Changes requested: Reviewers will either approve the PR or request changes. Almost all PRs will have at least some changes requested. PR authors address each comment, either by making the requested change or explaining why they think it is unnecessary. Once all comments are addressed, reviewers will re-review.
4. LGTM: A PR gets labeled LGTM ("looks good to me") when it has sufficient reviews. This means that a code owner from each modified file has approved. When multiple developers share code ownership, only one has to approve.
5. PR merged: PRs can be merged once CI checks pass and the LGTM label has been applied. Only members of the Oppia organization can merge PRs.

## Draft pull requests

While making a contribution, you may discover that your change is not complete and needs some more work. You can make a draft pull request to make it easy for other developers to give you feedback; however, draft pull requests consume resources like time on our CI runners, which slows down CI runs for other developers. Hence, you should prefix the commit messages with `[skip ci]` or `[ci skip]` to disable CI runs when those commits are going to a draft PR. If you want those tests to run to help you debug a problem, you should open a PR against your fork's `develop` branch instead of the `oppia/oppia` develop. This will still delay other developers' Circle CI runs, but not their GitHub Actions runs.

Learn more about skipping a [Travis CI build](https://docs.travis-ci.com/user/customizing-the-build/#skipping-a-build) and skipping a [Circle CI build](https://circleci.com/docs/2.0/skip-build/#skipping-a-build).

## Labeling issues and pull requests

While contributing to Oppia, you will need to add different labels to issues or pull requests which you are working on. However, not all labels are allowed on issues and pull requests. Below are labels which can be applied to pull requests:

* `dependencies`: Should be added to pull requests that updates one or more dependencies.
* `PR: Affects datastore layer`: Indicates that a PR changes the datastore layer. Adding this label notifies the developers in charge of datastore stability so they can review the PR.
* Changelog (labels containing `PR CHANGELOG`): Each PR should have one of these labels added to indicate what project this PR applies to. The developer mentioned in the label will be assigned to review the PR first.
* Labels starting with `PR: don't merge`: Indicate that some problem with the PR needs to be addressed before merging. For example, one of these labels gets added if the PR author hasn't signed the CLA yet.
* `PR: require post-merge sync to HEAD`: Should only be applied to pull requests which when merged will require all other open pull requests to be updated with the develop branch.
* `PR: for current release`: Identifies PRs that need to be included in the release that is currently in progress. This label is used by the release team to identify PRs to cherry-pick into the release.
* `PR: released`: Identifies PRs that have been cherry-picked into the release. Should only be used by the release team.
* `REVIEWERS: Please add changelog label`: When a new contributor opens a PR, they don't have permission to add labels. In that case, Oppiabot adds this label to tell reviewers to assign the appropriate changelog label.
* `stale`: This label gets added by oppiabot to PRs that have been inactive for a week. They will be automatically closed after 4 more days of inactivity.
* `PR: LGTM`: Indicates that a PR has all necessary approvals. The PR can be merged as soon as the CI checks pass.
* Other labels starting with `PR`.

All other labels are to be used on issues.

It should be noted that the **good first issue** label should only be added by members of the onboarding team.

A complete list of labels can be found [here](https://github.com/oppia/oppia/labels).

## Juggling multiple pull requests

After you've submitted a PR, and are waiting for it to get reviewed, you might want to start working on a new issue in the meantime. Git allows you to do this seamlessly! Always prioritize following up on your existing PRs and getting them ready for the next round of review. In particular, only start working on new issues/PRs after **all** the other PRs you're working on are in the "waiting for review" stage. This helps avoids creating a logjam in the build queues.
