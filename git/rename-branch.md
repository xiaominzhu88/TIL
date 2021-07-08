# Renaming Git Branch

🙌 Rename a Local and Remote Git Branch:

Switch to the `local branch` which you want to rename:

```jsx
git checkout <old_name>
```

Rename the `local branch` by typing:

```jsx
git branch -m <new_name>
```

👉 With those steps above, you have renamed the local branch.

<hr />

If you’ve already `pushed` the <old_name> branch to the remote repository , perform the next steps to rename the remote branch.

🦋 Push the <new_name> local branch and reset the upstream branch:

```jsx
git push origin -u <new_name>
```

Delete the <old_name> remote branch:

```jsx
git push origin --delete <old_name>
```

That’s it. 🤞
