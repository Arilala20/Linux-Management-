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
