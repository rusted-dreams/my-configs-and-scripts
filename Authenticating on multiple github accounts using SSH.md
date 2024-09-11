
---
tags: github
---

- Firstly generate the ssh key for the first account.
```shell
  ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/"acc1_name"
  ``` 

- Now the second key for the second account.
```shell
  ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/"acc2_name"  
```
- In the same directory where ssh keys have been generated i.e. `~/.ssh/`,
  To change the directory use the command `cd ~/.ssh/`, now create a config file using the command `notepad config`, this will create the config file and will open the file in notepad.

In the  notepad add the following lines.
```notepad
#account_1 : your 1st github account
Host github.com
 HostName github.com
 IdentityFile <~/ssh/acc1_name>

#account_2: your second github account name
Host github.com
 HostName github.com-<second account>
 IdentityFile <~/ssh/acc2_name>

```
**Note:** Anything inside `<>` are just place holders, replace it with your own info and save.

- start the ssh agent:
```shell
# run the command to start the ssh-agent
eval "$(ssh-agent -s)"

# add the private key to ssh agent
#1st one 
ssh-add <~/ssh/acc1_name>

# now the second one
ssh-add <~/ssh/acc1_name>
```


- Test your ssh connection:
```shell
ssh -T git@github.com
```

- now add the public key of the respective accounts to github

- Now when creating a new repository or adding a remote, If you want to use your first account the use as usual `git clone git@github.com:user/repo-name` but if you want to use your second account then, replace `github.com` with `github.com-<second account>`in the above code and it becomes `git clone git@github.com-<second account>:user/repo-name`. This time your second account will be used.
