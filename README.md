# Git course
In here are the files and instruction for the git course. You can find the initials setup you should have done before the course as well as some exercieses

In this course we will primarely focus on the CLI version of git in combination with GitHub. This is because I believe that while the cli has a steeper learning curve, it offers more flexibility and you can get a better understanding of the material through practising with the CLI while a gui might be easyer, it also gives an extra layer which can complicate things.

## Setup your computer's git
First, create an account on github.com.

### SSH Keys 
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

### GPG keys
First open your favorite unix (!!!!) terminal. Then you type the command:
```bash
gpg --full-generate-key
```
Then Select option 1 (RSA and RSA (default)), choose keysize 4096. Let the key expire after a year so type `3y`at the question for how long the key should be valid. Verify the correctness. Then type in your real name, a comment and an email adress that is associated with your github account. You can confirm the data or change something init. Now you will need to enter a parafrase, this is basically a password that you'll need for using this gpg key to sign your commits. Once you have done that you can check if the gpg key is added correctly by using hte command:
```bash
gpg --list-secret-keys --keyid-format=long
```
which will show you the gpg keys registered to your local machine. Now search for the string of numbers in the format `rsa4096/[GPG_id] 2024-08-22` where the last date will be the creation date of today. Copy this GPG_id into the command below. Please remember this **GPG_ID** for later.
```bash
gpg --armor --export [GPG_id]
```
This will result in a large block starting with the marks `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with the marks `-----END PGP PUBLIC KEY BLOCK-----`. Go ahead and copy all of this including the blocks. If you go to github.com > profile > settings > SSH & GPG keys > new GPG key, you can copy this in the text box with `key` above. Go ahead and give it a fun name. Please click safe.

Now you could of course save all your commits by typing `-S` all the time with all your commits. However, we don't want to do that so now we'll go to our last step. Make the signing automatic for all the commits. To do this you'll need to do two things. First, let's tell our system what key to use by using our GPG id again by the first of the two commands below. Then we tell our configuration to allways use the key by using the second command below. If you are really enthousiastic you could also tell git to sign your tags with the third command below.
```bash
git config --global user.signingkey [GPG_id]
git config --global commit.gpgSign true
git config --global tag.gpgSign true
```

Congrats! You are now all set up to use git in all it's glory!

## Exercise 1: Make your first branch
In this exercice we will be making our own branch. You can name the branch with the format `git<random-number>-<your_name>`. Sometimes organistaions have rules for what a branch should be named like. 

## Exercise 2: Your first commit
We are now ready to do a commit. Add a new file in the `Git Newbies` folder named with `your-name.txt`. Add some random text in the file if you feel likt it. Now it's time to add and commit the new file! Give your commit the commit message `<your name>'s first commit`

## Exercise 3: Your first PR
Now we need the new file in the main branch. Push your new branch to github and create a Pull Request. Then ask for a review.

## Exersice 4: All in once
Now create a new branch with the format `git2<random 3 letters>-<your_name>` and create a file with your name in the `Git greens` folder. Create a Pr and submit it for review.

## Exersice 5: Dealing with conflicts
Create a new branch again from the main. Wait untill you get the go-ahead from the trainer. Now add your name to the end and create a PR. Merge it in.

## Exersice 6: Dealing with Hubert's mistakes
