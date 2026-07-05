# Fix: Unable to Connect to a Virtual Machine Using Windows App
![RDP Connectivity Issue](https://github.com/MikeMilenk/RDP-Unable-to-Connect/blob/07df8cb7885e4dc54459d6813cc398741e46bb15/Images/1.png)

There are several reasons why you may be unable to connect to a virtual machine using **Windows App**. For example:

* Incorrect IP address or hostname.
* Incorrect credentials.
* Firewall restrictions.
* AD-DC is not running or shut down.
* The user is not allowed to connect via Remote Desktop.

During my troubleshooting, I was able to access the VM through the **Proxmox web console**, but I still could not connect using **RDP (or Windows App)**. This confirmed that the VM itself was running, so the issue was related to Remote Desktop configuration, user permissions, networking, or Windows settings.

I also found that if the computer is joined to an **Active Directory** domain, an offline **Domain Controller** can prevent domain users from authenticating over RDP.
![DC offline](https://github.com/MikeMilenk/RDP-Unable-to-Connect/blob/0b66f84284cce4790b4cfcad7fd9930ff243c2c5/Images/0.png)

In my case, the issue was that the user had not been added to the **Remote Desktop Users** local group.

## Steps

1. Open **Computer Management**.
2. Go to **Local Users and Groups** → **Groups**.
3. Open **Remote Desktop Users**.
4. Click **Add...**.
5. Enter the username you want to grant Remote Desktop access to (HOME/bdog in my case).
6. Click **Check Names** to verify the account.
7. Click **OK**, then **Apply**.
  ![Comp Mgmt Settings](https://github.com/MikeMilenk/RDP-Unable-to-Connect/blob/07df8cb7885e4dc54459d6813cc398741e46bb15/Images/2.png)
  ![Added user in RDUP](https://github.com/MikeMilenk/RDP-Unable-to-Connect/blob/07df8cb7885e4dc54459d6813cc398741e46bb15/Images/3.png)

## If You Receive an "Access is Denied" Error

You may see the following message:

> **Access is denied. The following error occurred while attempting to save properties to group "Remote Desktop Users" on computer "<ComputerName>".**
![Access Denied](https://github.com/MikeMilenk/RDP-Unable-to-Connect/blob/07df8cb7885e4dc54459d6813cc398741e46bb15/Images/4.png)

If that happens, make sure you are signed in with a **local administrator** account (or open **Computer Management** with administrative privileges) and repeat the steps above.

It may prompt you for the credentials of the user you want to add. Enter them.
![User's creds](https://github.com/MikeMilenk/RDP-Unable-to-Connect/blob/07df8cb7885e4dc54459d6813cc398741e46bb15/Images/5.png)

Once the user has been successfully added to the **Remote Desktop Users** group, try connecting again. This resolved the issue for me during my initial Windows App setup.
