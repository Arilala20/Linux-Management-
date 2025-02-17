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






#Introduction
This report documents my step-by-step execution of APT (Advanced Package Tool) commands for package management in Ubuntu. It covers system updates, installing packages, removing packages, managing repositories, and troubleshooting.

All commands, outputs, and explanations are included.

Part 1: Understanding APT & System Updates
1. Check APT Version
apt --version
Output: (apt --version apt 2.4.10 (amd64))

2. Update the Package List
sudo apt update
Explanation: This command fetches the latest package lists from configured repositories, ensuring we get the latest versions and security updates.

3. Upgrade Installed Packages
sudo apt upgrade -y
Difference between update and upgrade:

update: Refreshes the package list but doesn’t install updates.
upgrade: Installs the latest versions of all packages listed in the updated package list.
4. View Pending Updates
apt list --upgradable




✅ Why is this important?
Updating ensures that APT has the latest list of available package versions.

3️⃣ Upgrade Installed Packages
🔹 Command:

bash
Copy
Edit
sudo apt upgrade -y
🔹 Output:
Lists upgraded packages and applies updates.

✅ Difference between update and upgrade

apt update: Fetches the latest package list but does not install updates.
apt upgrade: Installs available updates for existing packages.
4️⃣ View Pending Updates
🔹 Command:

bash
Copy
Edit
apt list --upgradable
🔹 Output:
Lists packages that can be updated.

✅ Takeaway: Allows the user to check pending updates before running upgrade.

🔹 Part 2: Installing & Managing Packages
1️⃣ Search for an Image Editor
🔹 Command:

bash
Copy
Edit
apt search image editor
🔹 Output:
Shows a list of image editors.

✅ Selected Package: gimp

2️⃣ View Package Details
🔹 Command:

bash
Copy
Edit
apt show gimp
🔹 Output Highlights:

Version: 2.10.30
Dependencies: libgimp2.0, gimp-data, libgtk2.0
✅ Takeaway: Understanding dependencies is important to avoid missing libraries.

3️⃣ Install the Package
🔹 Command:

bash
Copy
Edit
sudo apt install gimp -y
🔹 Output:
Installation process completes successfully.

✅ Verification:
To check if the package is installed:

bash
Copy
Edit
apt list --installed | grep gimp
🔹 Output:

css
Copy
Edit
gimp 2.10.30-1ubuntu2 amd64 [installed]
🔹 Part 3: Removing & Cleaning Packages
1️⃣ Uninstall the Package
🔹 Command:

bash
Copy
Edit
sudo apt remove gimp -y
🔹 Output:
Removes gimp but keeps configuration files.

✅ Verification:

bash
Copy
Edit
apt list --installed | grep gimp
🔹 Output: Empty (package removed).

2️⃣ Remove Configuration Files
🔹 Command:

bash
Copy
Edit
sudo apt purge gimp -y
✅ Difference between remove and purge

remove: Deletes the package but keeps configuration files.
purge: Completely removes the package including config files.
3️⃣ Clear Unnecessary Dependencies
🔹 Command:

bash
Copy
Edit
sudo apt autoremove -y
✅ Purpose: Removes orphaned dependencies no longer needed.

4️⃣ Clean Up Downloaded Package Files
🔹 Command:

bash
Copy
Edit
sudo apt clean
✅ Purpose: Clears cached .deb files, freeing disk space.

🔹 Part 4: Managing Repositories & Troubleshooting
1️⃣ List All APT Repositories
🔹 Command:

bash
Copy
Edit
cat /etc/apt/sources.list
✅ Observation:
Lists all enabled software sources.

2️⃣ Add the Universe Repository
🔹 Command:

bash
Copy
Edit
sudo add-apt-repository universe
sudo apt update
✅ What is in universe?
Community-maintained software not officially supported by Ubuntu.

3️⃣ Simulate an Installation Failure
🔹 Command:

bash
Copy
Edit
sudo apt install fakepackage
🔹 Output:

vbnet
Copy
Edit
E: Unable to locate package fakepackage
✅ Troubleshooting:

Check if the package name is correct.
Run sudo apt update to refresh package lists.
Search available packages using:
bash
Copy
Edit
apt search fakepackage


"C:\Users\mayee\OneDrive\Pictures\Screenshots 1\Screenshot 2025-02-18 004023.png"

🔹 Bonus Challenge: Holding & Unholding Packages
1️⃣ Hold a Package
🔹 Command:

bash
Copy
Edit
sudo apt-mark hold firefox
✅ Purpose: Prevents firefox from being updated.

2️⃣ Unhold a Package
🔹 Command:

bash
Copy
Edit
sudo apt-mark unhold firefox
✅ Purpose: Allows firefox to receive updates again.

🔹 Why use hold?
Useful when new updates might break compatibility or cause system instability.

"C:\Users\mayee\OneDrive\Pictures\Screenshots 1\Screenshot 2025-02-18 004447.png"

