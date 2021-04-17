# Rename remote Branch

There isn’t a way to directly rename a Git branch in a remote repository. You will need to delete the old branch name, then push a branch with the correct name to the remote repository.

1. Verify the local branch has the correct name:

```jsx
git branch -a
```

2. Next, delete the branch with the old name on the remote repository:

```jsx
git push origin ––delete old-name
```

3. Finally, push the branch with the correct name, and reset the upstream branch:

```jsx
git push origin –u new-name
```

Alternatively, you can overwrite the remote branch with a single command:

```jsx
git push origin :old-name new-name
```

Resetting the upstream branch is still required:

```jsx
git push origin –u new-name
```
