# File Transfer In Python With SCP

# Article:
https://hackersandslackers.com/automate-ssh-scp-python-paramiko/

# Through Terminal

## For PC to Android

### Setup SSH with Android

#### 1. Install Termux
Termux Simulate a Linux Terminal in Android

https://play.google.com/store/apps/details?id=com.termux&hl=en

#### 2. Update your pkg manager:

Type 

```
pkg update && pkg upgrade
``` 

in the terminal and execute

#### 3. Install OpenSSH:

Type 

```
pkg install openssh
``` 

in the terminal and execute

#### 4. Create a password:

Type

```
pkg install termux-auth
```

```
passwd
```

in the terminal and execute and follow along

#### 5. Generate the SSH key

Type

```
ssh-keygen -A
```
in the terminal and execute

#### 6. Run the SSH Daemon:

Type
```
pkg install termux-services
. $PREFIX/etc/profile.d/start-services.sh   
sv-enable sshd
sv up sshd
sv status sshd
```
in the terminal and execute

On PC:

```
ssh -p 8022 <username>@<phone_ip>   
```
Because android port is strict so we use port 8022 instead of 22

find the username and ip with:
```
ifconfig
whoami
```

#### Bonus: Opening Shared Storage in Termux:
```
termux-setup-storage
```


### Start SCP files from PC to android

On Sender PC:

#### Create a text file or get any files to send and store it at ./files

```
mkdir files
sudo nano files/examples.txt
```

#### Send the files to android using SCP

```
scp -p 8022 ./files/examples.txt  <username>@<phone_ip>:~/
```

## For PC to PC:

### setup SSH on both PC

I am using Ubuntu so, I use apt package manager.

#### Instal OpenSSH
```
sudo apt update && sudo apt install openssh-server openssh-client
```

#### Start SSH Daemon background service:
```
sudo systemctl start sshd
```

#### Allow SSH on firewall port 22:
```
sudo ufw allow ssh
```

#### Setup SSH keys:
```
ssh-keygen -A
```

#### Connect with Host:

Go to receiving PC and check username and hostname:

Username:
```
whoami
```

Hostname:
```
hostname
```

Go to sender PC and execute:
```
ssh username@hostname
```

if works that means SSH has been set up

### Send file through SCP from PC to PC

On Sender PC:

#### Create a text file or get any files to send and store it at ./files

```
mkdir files
sudo nano files/examples.txt
```

#### Send the files to receiving PC using SCP

```
scp ./files/examples.txt  <username>@<phone_ip>:~/
```

# Through Python App:

Work in progress