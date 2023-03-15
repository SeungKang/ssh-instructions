# Connecting to Computer with SSH Public Key Authentication

**"server computer"** refers to the computer you are trying to connect to.
**"client computer"** refers to the computer you are connecting from.

## on client computer
Generate a key if you have not done so previously.

Open the Terminal application or Windows PowerShell

Create a SSH keypair by running the code contained in the block below
(note: the program will prompt you several times - use the defaults by typing the "enter" key):

```
ssh-keygen -t ed25519
```

Copy the public key file that was created in the `.ssh` directory in your user account (the file should be named: `id_ed25519.pub`)

### on server computer
    - install OS on Raspberry Pi
    - connect to a monitor and boot it up
    - setup ssh on sever
        - create a `.ssh` directory in the user directory `mkdir ~/.ssh`
        - within the `.ssh` directory create a file named `authorized_keys`
        - paste the client public key into the `authorized_keys` file as a new line
        - change the permissions on authorized_keys so that the user can only read and write with command `$ chmod 600 ~/.ssh/authorized_keys`
        - change the permissions for the `.ssh` directory with `$ chmod 600 ~/.ssh`
        - copy the server public key in the directory `/etc/ssh/ssh_host_ed25519_key.pub`
        - send this key to your client computer
            - via usb stick, email, messaging app
    - find out the IP address
        - you can use command `$ ping HOSTNAME.local`
    - to enable ssh
        - select the raspberry icon menu
        - select **Preferences** > **Raspberry Pi Configuration**
        - click the **Interfaces** tab
        - click the **Enabled** radio button for **SSH**
        
### on client computer
    - in the .ssh directory, create a file called `known_hosts` note that it has no file extension
        - file can be created without a file extension with command `$ touch known_hosts`
    - edit the `know_hosts` file using a text editor such as notepad or vim and paste the public key of the server into this file
    - in terminal or Windows PowerShell enter the command `ssh [username]@[sever IP]`
        - use the `-p` flag to specify port, default is 22 `ssh [username]@[sever IP] -p 24`
