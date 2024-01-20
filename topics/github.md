# When you commited and pushed to github but github shows two people in the commit.

This happens when your local repository `git config user.email` has email different from the one set in your github profile.

Set the same user email as in github profile by calling `git config user.email <same-email-as-in-github-profile>`.

Update commit by running

```
git commit --amend --author="Your Name <your github email>" --no-edit
git push origin -f main
```
