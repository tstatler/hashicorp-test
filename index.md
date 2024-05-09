## What is the difference between push, pull, and fetch?

You use the `git push,` `git fetch,` and `git pull` commands to synchronize changes between local and remote repositories.

- `git push` - Uploads changes in your local branch to the remote branch.
- `git pull` - Retrieves changes from the remote branch into your tracking branch and merges them into your local branch.
- `git fetch`— Retrieves changes from the remote branch into your tracking branch without merging them into your local branch.

### Git push

The `git push` command uploads changes in your local branch to the remote branch. This operation makes the remote branch identical to your local branch. It first checks that there is a remote-tracking branch for the remote repository connected to your local branch and then synchronizes local changes with the remote branch.

```bash
git push
```

If not all commits in the remote branch are in your local branch, the remote will reject the push operation, as shown below:

```bash
git push
To https://github.com/example/example.git
! [rejected]        feature-branch -> feature-branch
error: failed to push some refs to 'https://github.com/example/example.git'
```

In this case, you need to first synchronize your branch with the remote branch by either calling [`git pull`](#git-pull) or a combination of [`git fetch`](#git-fetch) and `git merge.`


### Git fetch

The `git fetch` command updates your remote-tracking branch with changes from the remote branch, but does not merge those changes into your local branch. This allows you to review the incoming changes before updating your working branch. It first checks for the existence of a corresponding remote-tracking branch (`origin/main,` for example). If one exists, it updates the tracking branch with the changes from the remote branch.

```bash
git fetch
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/example/example-repo
   cc57037..f91adc6  main       -> origin/main
```

Assuming you had the `main` branch checked out locally and `origin` was the remote name, you would run the following command to merge the fetched changes:

```bash
git merge origin/main
```

If you don't need or want to review remote changes before merging, you can use the [`git pull`](#git-pull) command, which combines `git fetch` and `git merge` in a single operation.

### Git pull

The `git pull` command calls [`git fetch`](#git-fetch) followed immediately by `git merge.` This is often what you desire to do, but some people prefer to use `git fetch` followed by `git merge` to make sure they understand the changes they are merging into their branch before the merge happens (see [`Git fetch`](#git-fetch)).

```bash
git pull
Updating cc57037..f91adc6
Fast-forward
 team.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 team.md
```
