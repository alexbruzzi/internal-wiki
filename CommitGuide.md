# Creating a new Repo

- Create a repo from phabricator UX. Allow SSH/HTTP authentications.
- Clone the repo locally to a dir. This dir would be called working directory. `cd` to your working directory.
- Create an empty commit

```
lang=bash
git commit --allow-empty -m "initial commit"
git push -u origin master
```
This step is crucial else it will cause errors while doing `arc land master` later on.

- Create the `.arcconfig` file. You may also copy it from one of the repos, as it contains the very basic set of minimal config to help you get started. Check the [guide](https://secure.phabricator.com/book/phabricator/article/arcanist_new_project/) for exhaustive details. A minimum `.arcconfig` should contain the following

```
lang=json
{
  "phabricator.uri" : "http://phab.octo.ai/"
}
```

# Making your changes

## Documentation Stats

After you make changes to your code, and have done the documentation, run the following to see the documentation coverage

```
yard stats
```

# Sending your changes

## Creating diff

- clone the repo
- make changes
- `git commit`. While creating your commit message you **must reference the Task against which this is being committed**. Attach to a task with "Ref", "Refs", "References" or "cf." These are hard-coded and case insensitive. This works in Differential and commits. For example, writing Ref T123 in a revision summary will attach that revision to task T123. [Reference](https://secure.phabricator.com/T5132#69200)
- create a diff using `arc diff`. Add the test plan, staging, reviewers and other necessary details.

If there are changes requested, do the following

- make the changes
- commit the changes `git commit`
- create a diff `arc diff`. It will automatically update with the same differential number.

If your changes are approved, you need to see Landing Commits below.

## Landing commits

If your changes are accepted by the reviewers, you need to land your commits.

- `arc land master`

If you have phab pointed as a different remote (than origin), then use the following

- `arc land master --remote your_remote_name`

# Reviewing Diff

## Approving

- Go to differential page, and the `Leap into Action` section. Select the `accept review` option. Optionally, add a comment.

## Requesting Changes

- Go to differential page, and the `Leap into Action` section. Select the `request changes` option. Do add a comment mentioning the changes requested.


# Troubleshooting

- [Arc Diff Guide](https://secure.phabricator.com/book/phabricator/article/arcanist_diff/)
- [.arconfig Guide](https://secure.phabricator.com/book/phabricator/article/arcanist_new_project/)
- [Differential Guide](https://secure.phabricator.com/book/phabricator/article/differential/)
