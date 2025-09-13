# Issues

Document issues and fixes if they were found.

## Push Command Not Working

When running `git push origin main` in CLI, the console will ask for GitHub username and password.
After inputting all correct information the following error is received:
```
remote: Password authentication is not available for Git operations.
remote: You must use a personal access token or SSH key.
```

I realized since I already created my SSH key and that I validated the SSH connection with `ssh -T git@github.com` successfully.  I needed to find a way to ensure any changes were done through the SSH token and not via user authentication.

I found the following command `git remote set-url origin git@github.com:username/your-repository.git`. 

This fix was found [HERE](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278).
