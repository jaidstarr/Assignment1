# Assignment1
**setting up your first droplet and SSH key**

**What is an SSH Key?**

SSH keys, also known as Secure Shell keys, are authentication credentials used to manage networks, operating systems, and configurations. When implemented correctly, they provide a strong and secure method of user authentication.

In simple terms, SSH keys automate the verification process and are often used for single sign-on (SSO), allowing users to access multiple systems or applications with a single set of credentials. Each SSH key pair consists of two keys: a public key, which can be shared with others, and a private key, which is securely kept by the owner.

**Creating an SSH key on windows 11:**

1. Open Windows PowerShell.

you will need to create a .ssh directory in your home directory, if you don't have one already.
2. type `cd ~` and hit **Enter** to get to your home directory.

3. type `mkdir .ssh` and hit **Enter** to create your .ssh directory.

once you have created a .ssh directory, you can start creating your SSH key pairs. 

4. type ``ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\example-key -C "youremail@email.com"`` into the terminal and hit **Enter**

be sure to replace "your-user-name" with the username associated with your computer as well as "example" as the desired name of your key. this command will create for you the 2 text files you need, inside your .ssh directory. 
![image](https://github.com/user-attachments/assets/8caac262-aed8-49c4-8c27-ce5dbfaa4c60)

5. Type a desired password into the terminal, or press **Enter** twice to skip. it is recommended that you set a password.

once your key pairs are created successfully, you will receive this output. 
![image](https://github.com/user-attachments/assets/45975851-1f24-4afb-8239-1044a1e13229)



To see your files inside of your .ssh directory.

6. type `cd .ssh` and press **Enter**
   
7. type `ls` and press **Enter**
   
the `ls` command will print out all files in the directory you are currently located in. In this list there should be your "example-key" along with your "example-key.pub"
![image](https://github.com/user-attachments/assets/77073659-31d1-4e01-9362-79d7fdae9717)


Your SSH key pair has been created successfully. 

**Downloading an Arch Linux Image**

we are now going to add a custom Arch Linux Image. Arch linux is a Linux distribution.
1. Click
	https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages/1545 
	to be directed to the Arch Linux download.
  there will be many options to chose from, so double check you have the right one. 
3. click on the image that is named:
	Arch-Linux-x86_64-cloudimg-20240915.263127.qcow2
![image](https://github.com/user-attachments/assets/e58b8f0c-5337-4e85-abc6-aef163d8474a)

	once the image is successfully downloaded we can move onto creating a droplet on Digital Ocean.

**Uploading your Arch Linus Image onto Digital Ocean**

1. Click **Create** on the top right of your screen.

2. Click **Droplets**

   ![image](https://github.com/user-attachments/assets/541e188b-76a5-4cc2-a2fb-ee1d0e603d16)

4. Click **San Francisco** and make sure **SFO3** is selected in the dropdown.![image](https://github.com/user-attachments/assets/a088b42e-ceee-49df-947b-53ee60b9794a)

5. Scroll down to **Choose an image**

6. Click **Custom images**

7. Click **Add image**

   ![image](https://github.com/user-attachments/assets/544cbc05-9751-454b-89b5-d0e9ce39e685)

9. Click **Upload Image** and chose the Arch Linux image that you previously downloaded. 
10. Click **Choose a Distribution** and select **Arch Linux** from the drop down.   ![image](https://github.com/user-attachments/assets/533b0af7-b5ec-4d9d-baa3-7dedbf6d059e)

11. Click **Upload Image** at the bottom of the page.


**Setting up your Droplet**

Now that your Arch Linux Image is uploaded, you can create your first droplet. a droplet is Digital Oceans name for a Linux virtual environment.

1. Click your Arch Linux custom image ![image](https://github.com/user-attachments/assets/3c4d596a-a144-428c-b78f-17c0b592b76b)

2. Click your preferred settings, pictured below is an example, but any set up will work.![image](https://github.com/user-attachments/assets/fe4ded90-fb78-425a-ac81-1e72917b1ee0)


In the **Choose Authentication Method** section, you are going to set up you SSH key you have created. 

1. Open **Windows PowerShell**
2. Type `code example-key.pub` into the terminal. 

this will open the content of the SSH key. Copy the contents of the file to your clipboard. the contents should be like this string given below:

![image](https://github.com/user-attachments/assets/b11d449d-7ed1-4ba3-882e-0ee990ce3b1f)


**In Digital Ocean:**
1. Click **SSH Key**
2. Click **New SSH Key**![image](https://github.com/user-attachments/assets/7411b724-b3f3-4439-8ce1-85f8f53c9103)

3.  Paste you SSH key contents into the given box.
4. Type a name for your key in the **Name** box
5. Click **Add SSH Key**
   
Your SSH key has been added to your droplet!

**To set up your droplet with cloud-init:**
to create a cloud-init file for a droplet, the best way is to use a YAML file. 
1. Click **Advanced Options**
2. Click **Add Initialized scripts**
   
![image](https://github.com/user-attachments/assets/b3c242c8-0f2a-4209-8f17-8be8afc97700)

in the box provided you can then add your configuration.

3. Copy and Paste the below YAML file inot the user data box.
```
users:
  - name: #add name
    primary_group: #add group
    groups: wheel
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-ed25519 ...

packages:
  - ripgrep
  - rsync
  - neovim
  - fd
  - less
  - man-db
  - bash-completion
  - tmux

disable_root: true

```

4. Click **Add Droplet** in the bottom right.

the droplet has now been created successfully.





