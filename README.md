# Fix: Unable to Connect to a Virtual Machine Using Windows App

There are several reasons why you may be unable to connect to a virtual machine using **Windows App**. For example:

* Incorrect IP address or hostname.
* Firewall or browser-related issues (I ran into Firefox-related issues during the initial setup).
* Incorrect credentials.
* The user is not allowed to connect via Remote Desktop.

In my case, the issue was that the user had not been added to the **Remote Desktop Users** local group.

## Steps

1. Open **Computer Management**.
2. Go to **Local Users and Groups** → **Groups**.
3. Open **Remote Desktop Users**.
4. 
5. Click **Add...**.
6. Enter the username you want to grant Remote Desktop access to.
7. Click **Check Names** to verify the account.
8. Click **OK**.
9. Click **Apply**, then **OK**.

## If You Receive an "Access is Denied" Error

You may see the following message:

> **Access is denied. The following error occurred while attempting to save properties to group "Remote Desktop Users" on computer "<ComputerName>".**

If that happens, make sure you are signed in with a **local administrator** account (or open **Computer Management** with administrative privileges) and repeat the steps above.

Once the user has been successfully added to the **Remote Desktop Users** group, try connecting again. This resolved the issue for me during my initial Windows App setup.
