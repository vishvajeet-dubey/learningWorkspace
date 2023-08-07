# learningWorkspace

HOW TO INSTALL THE RABBITVCS
------------------------------
RabbitVCS is a set of graphical tools written to provide simple and straightforward access to the version control systems you use. We provide multiple clients and extensions designed to give you a uniform experience no matter what development tools you use. 



Below are the offical link for rabbit
* [Download](http://wiki.rabbitvcs.org/wiki/install/ubuntu)


Below are the installation steps<br>
```
sudo add-apt-repository ppa:rabbitvcs/ppa
sudo apt-get update
sudo apt-get install rabbitvcs-nautilus
nautilus -q
```


Uninstall the RABBITVCS
------------------------------
```
sudo apt-get purge rabbitvcs*
```


First time Configuration
------------------------------
Add the git config 
```
git config --global user.email "contact.vdubey@gmail.com"
git config --global user.name "vishvajeet-dubey"
```

Show the saved config
```
git config --list
```



Adding the ssh Key in github
------------------------------
Please follow the below steps 
1. open terminal
2. Paste the text below, substituting in your GitHub email address.
```
ssh-keygen -t ed25519 -C "contact.vdubey@gmail.com"
```
3. Press enter 2 times 



Adding your SSH key to the ssh-agent
------------------------------

STEP 1
```
eval "$(ssh-agent -s)"
```
output: Agent pid 55798

STEP 2
```
ssh-add ~/.ssh/id_ed25519
```
output: Identity added: /home/vishva/.ssh/id_ed25519 (contact.vdubey@gmail.com)



Setting the remote link
------------------------------
```
git remote set-url origin git@github.com:vishvajeet-dubey/learningWorkspace.git
```


Authorizing an SSH key
----------------------------
Please open the below link to update the ssh key in GitHub ssh
[link](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/authorizing-an-ssh-key-for-use-with-saml-single-sign-on)


**END**
