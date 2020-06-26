After a while you'll get notifications about comments on your pull requests from your reviewers. Often times, you'll need to change something before the branch is ready.

## Solving change requests
Change requests should be applied in separate _fixup_ or _squash_ commits. Rebaseing the branch during an ongoing review is not appreciated unless there is a good reason for it, like pulling in some new and necessary changes from `master`, because it makes harder for the reviewers to know what the new changes are and what they already reviewed.

These commits should be merged into `staging` as well when they are done.

## Merging

### Staging
Once the PR is opened, the branch can be merged into `staging`, unless it contains considerable
logic in the migrations, in which case the reviewers should prioritize reviewing the migrations
first, and giving a thumbs up before merging.

We have 2 ways of doing branch merges to `staging`:
1. Merge & squash
2. Cherry-picking a commit range

#### Merge squash

```bash
git switch staging
git fetch origin staging && git pull --rebase
git merge --squash {branch-name}
```

#### Cherry-picking

```bash
git switch staging
git fetch origin staging && git pull --rebase
git cherry-pick -n {BASE-OF-BRANCH}..{branch-name}
```

_Note_: BASE-OF-BRANCH is one commit prior of the first commit of the branch.

Cherry picking usually produces less merge conflicts once `master` and `staging` diverge.

The commit message should be in the following format.
```
Merge-squash {branch-name}

(pull request {pull-request-link})
[optionally](cherry picked from {commit-sha})
```

Including the pull request link in the message results with a reference in the pull request feed, which is helpful because we'll know when the branch was deployed to `staging`.

Make sure that everything's ok by running the specs, then push.

#### Keep it clean
After a while the `staging` branch history can become quite different than `master`, because of the different branch merges. You'll sometimes even find yourself pushing a couple of _fixup_ commits to `staging` if you're fixing something and then applying the changes to the `fix/branch`.

We are resetting the `staging` branch to `master` after each sprint, or more frequently as we see fit:

```bash
git switch staging
git reset --hard origin/master
git push origin staging --force
```

### Master
Once the PR has at least 1 approval, the branch was successfully deployed to `staging` and tested, and
there are no failing specs, it can be merged into `master`.

We are doing non fast forward merges to group commits of a single feature together in a meaningful
way. Before merging we're also rebasing the feature branch on the latest `master`, so that the git
history is nice and clean, and that the latest code can be run on CI before actually merging into
`master`. We're also squashing the review comments corrections here, so make sure the `--autosquash`
option is on by default or add that flag to the rebase command.

While on feature branch:
```bash
git fetch origin master
git rebase -i origin/master
git push --force
```

Then, check once again that everything is squashed correctly and continue on the `master` branch:

```bash
git fetch origin master
git switch master && git pull
git merge --no-ff --no-edit {branch-name}
```

Make sure the history graph is nice and clean by entering the following command or similar and
making sure that no lines "cross over".

```bash
git log --oneline --graph
```

Bad:

```bash
*   1b82b9f (HEAD -> master) Merge branch 'feature/add-git-process-to-readme'
|\
| * a25b3dc (origin/feature/add-git-process-to-readme, feature/add-git-process-to-readme) Add git process to readme
* |   bfe1152 (origin/master) Merge branch 'feature/xx-some-other-feature'
|\ \
| |/
|/|
| * 3345dbb Some other feature subject
|/
*   7eade95 Merge branch 'feature/xx-another-other-feature'
|\
| * 0a80385 Another feature subject
|/
*
```

Good:

```bash
*   1a164b4 (HEAD -> master) Merge branch 'feature/add-git-process-to-readme'
|\
| * 497dcd7 (origin/feature/add-git-process-to-readme, feature/add-git-process-to-readme) Add git process to readme
|/
*   bfe1152 (origin/master) Merge branch 'feature/xx-some-other-feature'
|\
| * 3345dbb Some other feature subject
|/
*   7eade95 Merge branch 'feature/xx-another-other-feature'
|\
| * 0a80385 Another feature subject
|/
*
```

Make sure that everything's ok by running the specs, then push.
