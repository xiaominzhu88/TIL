# Git Merge Rebase

- Merging takes the contents of a source branch and integrates them with a target branch. In this process, <b>only the target branch is changed</b>. The source branch history remains the same.

Merge the master branch into the feature branch using the checkout and merge commands.

```jsx
$ git checkout your-branch
$ git merge master

(or)

$ git merge master your-branch
```

This will create a new “Merge commit” in the feature branch that holds the history of both branches.

- Rebase compresses all the changes into a single “patch.” Then it integrates the patch onto the target branch.

Rebase the feature branch onto the master branch using the following commands.

```jsx
$ git checkout your-branch
$ git rebase master
```

This moves the entire feature branch on top of the master branch. It does this by re-writing the project history by creating brand new commits for each commit in the original (feature) branch.

☘️ **Your code is ready for review**: You created a pull request. Others are reviewing your work and are potentially fetching it into their fork for local review. At this point, **you should not rebase your work.** You should create ‘rework’ commits and update your feature branch.
