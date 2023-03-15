# Connecting to Computer with SSH Public Key Authentication

**"Server"** refers to the computer you are trying to connect to. (Raspberry Pi)

**"Client"** refers to the computer you are connecting from. (Desktop PC)

## On the Client Machine
If you have not generated a private and public key, known as a *key pair* previously then follow these instructions. Otherwise skip to the "On the Sever Machine" section.

1. Open the Terminal application or Windows PowerShell
2. Create a SSH keypair by running the code contained in the block below (note: the program will prompt you several times - use the defaults by typing the "enter" key):

```
ssh-keygen -t ed25519
```
3. Enter the passphrase to encrypt the private key. Re-enter the same passphrase and press **Enter** to finish generating the key pair. 
4. Copy the public key file that was created in the `.ssh` directory in your user account (the file should be named: `id_ed25519.pub`). This key will be added to the sever in the following steps.

## On the Server Machine
5. Install OS on Raspberry Pi
6. Boot it up and connect to internet
7. Open the Terminal
8. Create a `.ssh` directory in the user directory 
    ```
    mkdir ~/.ssh
    ```
9. Within the `.ssh` directory create a file named `authorized_keys`
    ```
    touch ~/.ssh/authorized_keys
    ```
10. Open the `authorized_keys` file using a text editor such as Text Editor, Notepad or VIM. Paste the client public key into the `authorized_keys` file as a new line
    ```
    vim ~/.ssh/authorized_keys
    ```
11. Change the permissions on authorized_keys so that the user can only read and write.
    ```
    chmod 600 ~/.ssh/authorized_keys
    ```
12. Change the permissions for the `.ssh` directory
    ```
    chmod 600 ~/.ssh
    ```
13. Copy the server public key in the directory `/etc/ssh/ssh_host_ed25519_key.pub`. Can use the command `cat` to print key to the terminal as shown below.
    ```
    cat /etc/ssh/ssh_host_ed25519_key.pub
    ```
14. Send this public key to your client computer via usb stick, email, messaging app.
15. Determine the Server IP address. You can use the command 
    ```
    hostname -I
    ```
16. To enable SSH
    - select the raspberry icon menu
    - select **Preferences** > **Raspberry Pi Configuration**
    - click the **Interfaces** tab
    - click the **Enabled** radio button for **SSH**
        
### On Client Machine
17. In the `.ssh` directory, create a file called `known_hosts` note that it has no file extension
18. Edit the `know_hosts` file using a text editor and paste the public key of the server into this file
    ```
    vim ~/.ssh/known_hosts
    ```
19. In terminal or Windows PowerShell enter the command
    ```
    ssh [user]@[sever IP]
    ```
20. The connection will prompt for the password created in Step 3

Once the connection is established, you can manage the virtual server remotely from your computer :)