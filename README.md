# Git course
In here are the files and instruction for the git course. You can find the initials setup you should have done before the course as well as some exercieses

In this course we will primarely focus on the CLI version of git in combination with GitHub. This is because I believe that while the cli has a steeper learning curve, it offers more flexibility and you can get a better understanding of the material through practising with the CLI while a gui might be easyer, it also gives an extra layer which can complicate things.

## Setup your computer's git
First, create an account on github.com.

Then go to your preferred CLI for mac and Linux the commands are below. In Windows you can use the linux commands in git bash or install ubuntu. We start with generating a keypair.
```bash
mkdir .ssh | ssh-keygen -t ed25519 -C <your@email.nl> -f ~/.ssh/gitkey
```
Where you can replace `<your@email.nl>`

Then press enter through the questions. We now created a ssh keypair. We now need to tell our system to actually use this keypair.

For Linux or macOS we can do add the keypair with the following line
```bash
eval "$(ssh-agent -s)" | ssh-add ~/.ssh/gitkey
``` 
On macOS and some linux distributions you might also need to add it to a config file. You can do that with the command:
```bash
touch ~/.ssh/config | printf "\nHost github.com\n  AddKeysToAgent yes\n  IdentitiFyile ~/.ssh/gitkey\n" >> ~/.ssh/config
```
Now you can with the following command see the public key you generated. You can add the public key to your github account by going to github.com > click on the profile picture > settings > SSH & GPG keys > New SSH Key. Give yoru SSH key a nice name and past the output of the following command (Linux):
```bash
cat ~/.ssh/gitkey.pub
```

## Exercise 1: Make your own branch
In this exercice we will be making our own branch. You can name the branch with the format `git<random-number>-<your_name>`. Sometimes organistaions have rules for what a branch should be named like. You can create a branch with the commands
```bash
git checkout -b <branch-name>
```




