# Git Merge Abort

Run into a merge conflict with 'git pull', abort the merge

If your git version is >= 1.6.1, you can use

```jsx
git reset --merge
```

If your git version is >= 1.7.4, you can also use

```jsx
git merge --abort
```

**As always, make sure you have no uncommitted changes before you start a merge.**

☘️ "git merge --abort" is equivalent to "git reset --merge", when "MERGE_HEAD" is present, "MERGE_HEAD" is present when a merge is in progress.
