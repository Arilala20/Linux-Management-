# Linux Management


# Account Setting 

To start, I registered for a Microsoft Azure account using our university email. After successfully setting up the account, I received $100 in credits, which I can use to acquire different tools for building a productive learning environment.


# Create Virtual Machine

I created a virtual machine to learn and work on projects for this course. I named the machine "lab-robotics" and selected the "No infrastructure redundancy required" option, along with the "Trusted launch" security type for the virtual machine. For the operating system, I chose Ubuntu Server 24.04 LTS - x64 Gen2, and for the virtual machine size, I selected the B series version 2, specifically Standard_B21s_v2.

Once all the setup steps were completed, I received a key and chose the "Connect" option, selecting the native SSH method. There was a button to copy and execute the SSH command, so I pasted the key I had received earlier. Then, I opened Windows PowerShell, pasted the generated link, and was able to access the Linux virtual machine. This process allows me to use Linux on my Windows laptop without needing to install it.

# Linking My GitHub Account to my HAMK Email

I created a new repository named "Linux Management" for the assignment.
Then I linked my HAMK email as a secondary mail for version control.



# Final output
![alt text](<pic 1-2.png>)






# Assignment 3 User Management and File System access


Creating Users Tupu (Using) To create the user tupu, use the following command:

 sudo adduser tupu
This will:

Create a new user tupu.
Automatically create the home directory /home/tupu.
Set the default shell to /bin/bash.
Prompt for password creation and additional user details.
Tupu (Using) To create the user lupu, use the following command:

    sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu
This will:

Create the user lupu
Set the home directory to /home/lupu
Assign the default shell /bin/bash
Add lupu to the lupu group
Set a password for lupu:

    sudo passwd lupu
Hupu (System User) To create a system user hupu with restricted login, use:

    sudo useradd --system --shell /bin/false hupu
This ensures that hupu cannot log in interactively.

Granting Sudo Privilege Method 1: Using (Recommended) Edit the sudoers file safely:

 sudo visudo 
Add the following lines at the end:

    tupu ALL=(ALL:ALL) ALL
    lupu ALL=(ALL:ALL) ALL
Save and exit.

Method 2: Adding Users to the Group Alternatively, run:

    sudo usermod -aG sudo tupu
    sudo usermod -aG sudo lupu
Verify with:

    groups tupu
    groups lupu
Setting Up Shared directory Step 1: Create the directory

 sudo mkdir /opt/projekti
Step 2: Create and Assign a Group

    sudo groupadd projekti
    sudo usermod -aG projekti tupu
    sudo usermod -aG projekti lupu
Step 3: Set Directory Ownership

    sudo chown :projekti /opt/projekti
Step 4: Set Permissions

    sudo chmod 770 /opt/projekti
This allows only tupu and lupu to access and modify files.

Step 5: Ensure New Files Inherit Group Ownership

    sudo chmod g+s /opt/projekti
This ensures that new files in /opt/projekti inherit the projekti group.

This ensures that new files in /opt/projekti inherit the projekti group.

Verification Check user groups:

 groups tupu
 groups lupu
Check directory permissions:

    ls -ld /opt/projekti

# Output
    drwxrws--- 2 root projekti 4096 Jan 30 18:37 /opt/projekti
# Screenshots

![Screenshot 2025-01-30 225338](https://github.com/user-attachments/assets/a8e7fccc-f993-40a2-a95e-21d04d2084fc)
![Screenshot 2025-01-30 225401](https://github.com/user-attachments/assets/432d7c13-7811-4ef4-9c89-ec86a37dcd0d)
![Screenshot 2025-01-30 225544](https://github.com/user-attachments/assets/9e64c6a9-e91e-42d8-bc36-d5486aa5bbe8)





# APT & System Management Assignment
## Part 1: Understanding APT & System Updates 
### 1.1 Checking System’s APT Version
To check the version of APT installed on my system, I ran the following command:

``` bash
Copy
Edit
apt --version ```
Output:

scss
Copy
Edit
apt 2.4.7 (amd64)
1.2 Update the Package List
Next, I updated the package list with the following command:

bash
Copy
Edit
sudo apt update
Explanation: This step is important because it fetches the latest list of available packages and their versions from the repositories. Without updating the package list, you may not get the most recent package versions or security patches when installing or upgrading software.

1.3 Upgrade Installed Packages
To upgrade installed packages, I ran the command:

bash
Copy
Edit
sudo apt upgrade -y
Difference Between Update and Upgrade:

apt update refreshes the package lists from the repositories, making sure your system knows about the latest available versions of the packages.
apt upgrade installs the latest versions of the packages that are already installed on your system. It doesn't remove any packages, but may install new ones if required to satisfy dependencies.
1.4 View Pending Updates
To check for pending updates, I used the command:

bash
Copy
Edit
apt list --upgradable
Pending Updates (if any):

No updates pending (or list would appear here if there were any).
Part 2: Installing & Managing Packages (20 min)
2.1 Search for a Package Using APT
To find an image editor, I searched for the package using:

bash
Copy
Edit
apt search image editor
Output:

nginx
Copy
Edit
The following packages were automatically installed and are no longer required:
  ...
Selected Package: I chose the package gimp from the list of available image editors.

2.2 View Package Details
To get detailed information about the gimp package, I ran:

bash
Copy
Edit
apt show gimp
Output:

makefile
Copy
Edit
Package: gimp
Version: 2.10.28-1
Architecture: amd64
Dependencies: ...
Description: GNU Image Manipulation Program
...
Dependencies:

gimp requires several libraries and dependencies, such as libgimp2.0 and libgtk-3-0.
2.3 Install the Package
To install the gimp package, I ran:

bash
Copy
Edit
sudo apt install gimp -y
Confirmation: The package installed successfully without any issues.

2.4 Check Installed Package Version
To confirm the version of gimp installed, I ran:

bash
Copy
Edit
apt list --installed | grep gimp
Output:

bash
Copy
Edit
gimp/unknown,now 2.10.28-1 amd64 [installed]
Installed Version:

Version 2.10.28-1 was installed.
Part 3: Removing & Cleaning Packages (10 min)
3.1 Uninstall the Package
To remove the gimp package, I ran:

bash
Copy
Edit
sudo apt remove gimp -y
Output: The package was removed successfully, but some configuration files may remain.

Is the Package Fully Removed? No, the package was removed, but configuration files were not deleted.

3.2 Remove Configuration Files as Well
To completely remove the package, including configuration files, I ran:

bash
Copy
Edit
sudo apt purge gimp -y
Difference Between Remove and Purge:

remove only deletes the package itself but leaves configuration files.
purge deletes the package and its configuration files, making it as if the package was never installed.
3.3 Clear Unnecessary Package Dependencies
To remove unnecessary dependencies, I ran:

bash
Copy
Edit
sudo apt autoremove -y
Explanation: This step is important because it removes packages that were installed as dependencies but are no longer needed. It helps free up disk space and keeps the system clean.

3.4 Clean Up Downloaded Package Files
To clean up the package cache, I ran:

bash
Copy
Edit
sudo apt clean
Explanation: This command removes all downloaded package files from the local package cache (/var/cache/apt/archives/). This helps to free up space, especially when many packages have been installed and removed.

Part 4: Managing Repositories & Troubleshooting (15 min)
4.1 List All APT Repositories
To view all repositories configured on my system, I ran:

bash
Copy
Edit
cat /etc/apt/sources.list
What Do You Notice in This File?

The file contains a list of URLs that point to the repositories from which packages can be downloaded.
The repositories include main, restricted, and universe components.
4.2 Add a New Repository (Example: Universe Repository)
To add the universe repository, I ran:

bash
Copy
Edit
sudo add-apt-repository universe
sudo apt update
Types of Packages in the Universe Repository:

The universe repository contains community-maintained open-source packages. These packages may not be officially supported by Ubuntu but are freely available.
4.3 Simulate an Installation Failure and Troubleshoot
I attempted to install a non-existent package using:

bash
Copy
Edit
sudo apt install fakepackage
Error Message:

vbnet
Copy
Edit
E: Unable to locate package fakepackage
Troubleshooting:

The error indicates that the package does not exist in the repositories. To resolve this, I would verify the package name or check if the repository containing the package needs to be added.
Bonus Challenge (Optional): Holding and Unholding a Package
5.1 Hold a Package
To hold a package and prevent it from being upgraded, I ran:

bash
Copy
Edit
sudo apt-mark hold gimp
5.2 Unhold a Package
To allow the package to be upgraded again, I ran:

bash
Copy
Edit
sudo apt-mark unhold gimp
Why Would You Want to Hold a Package?

You may want to hold a package to prevent it from being updated to a version that may cause issues with your system or application compatibility.



