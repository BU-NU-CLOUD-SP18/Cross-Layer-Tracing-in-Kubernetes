# Step 0: Creating SSH keys(for Linux&macOS)

(1)Open a terminal and run:

	Cd ~/.ssh

   If this directory dose not exist, skip (2).

(2)Check if you have a key already:

	ls id_*

   If you have already had a key, skip instruction below.

(3)If not, create a new key: 

	ssh-keygen -t rsa -C "your_email@example.com"

(4)After seeing a response, press <enter> to accept the default location and file name.
 
   Enter, and re-enter, a passphrase when prompted.

   Then your are all set.



# Step 1: Create an instance

(1)Log into MOC, go to instance under compute tag, choose "launch instance".

(2)Follow the steps in the box. When it comes to Key pair, choose "import key pair" and 

   upload public key pair you created in Step 0. Choose a floating IP for this instance. 

   Follow the steps, and choose "launch instance". 



# Step 2: Create a cluster

(1)Log into your new instance using the command:

	ssh username*@'floating_ip of your instance

(2)Create a key-pair on the instance.

(3)Switch to the ssh folder with: 

	cd ~./ssh
   Open the public key file and copy its content.

(4)Import key we just created on OpenStack. Click on 'Import Key Pair'

(5)Add the name you want and paste the public key into the public key section.

   Then click on 'Import Key Pair'.

(6)Create a worker node like step 2. Notice that The master node and the worker node  

   should be on the same network. At the Key Pair section choose the key you created in 

   (2). You can launch as many workers as you want.

What we have done is basically injected the public key of the master node (the first instance you launched) into the authorized_keys file on every node in your cluster. This way your master always has password-less ssh access into your nodes.


 




