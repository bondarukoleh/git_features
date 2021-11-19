### Multiple github accounts

1. You need a couple of ssh key for your second github account
```shell
ssh-keygen -t rsa -C "your-email-address"
```

2. Add new created .pub key to your second github account
3. Create `~/.ssh/config` file
```text
# My github account: oleh
Host github.com
   HostName github.com
   IdentityFile ~/.ssh/id_home
   IdentitiesOnly yes
   
# Work github account: olehSecond
Host github-secondAccountGitHubOrganization.com
   HostName github.com
   IdentityFile ~/.ssh/id_second
   IdentitiesOnly yes
```
4. Create the `.gitconfig` for second account in `someFolder` folder.
```text
[user]
	name = Oleh Bondaruk
	email = olehbondaruk@secondMail.com

```
5. Add a note about your second account in main `.gitconfig`
```text
[user]
	name = Oleh Bondaruk
	email = olehbondaruk@mainMail.com

[includeIf "gitdir:/C/path/to/second/acc/projects/*"]
    path = ~/someFolder/.gitconfig
```

6. Register added key with `ssh-agent`
```shell
# start agent on windows
eval `ssh-agent -s`

# register key
ssh-add ~/.ssh/id_second
```

7. Clone the repo
When you clone the repo for 2nd acc, remember that you need to modify the command you've copied and pasted from GitHub.
Instead of `git clone git@github.com:someOrganization/repo.git` <br>
Use `Host` from `~/.ssh/config` file
```shell
git clone git@github-secondAccountGitHubOrganization.com:someOrganization/repo.git
```
