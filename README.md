# YTL

https://www.youtube.com/watch?v=S1a7RmqeZ5E

https://www.youtube.com/watch?v=COp6JtP45o8

https://www.youtube.com/results?search_query=how+ssh+normal+user+on+linux




Here are the steps to create a non-root user who can SSH into an AWS Ubuntu VM from a local machine using another key:

Log in to the AWS Ubuntu VM as the root user.

Create a new user with the desired username using the following command:

php
Copy code
sudo adduser <username>
Replace <username> with the desired username for the new user.

Set a password for the new user using the following command:

php
Copy code
sudo passwd <username>
Replace <username> with the username you created in step 2.

Switch to the new user using the following command:

php
Copy code
su - <username>
Replace <username> with the username you created in step 2.

Generate a new SSH key pair on the local machine using the following command:

Copy code
ssh-keygen -t rsa
Follow the prompts to save the key pair to the desired location.

Copy the public key to the AWS Ubuntu VM using the following command:

vbnet
Copy code
ssh-copy-id -i /path/to/public/key <username>@<aws-vm-ip-address>
Replace /path/to/public/key with the path to the public key file you generated in step 5, <username> with the username you created in step 2, and <aws-vm-ip-address> with the IP address of the AWS Ubuntu VM.

Test the SSH connection from the local machine using the following command:

vbnet
Copy code
ssh -i /path/to/private/key <username>@<aws-vm-ip-address>
Replace /path/to/private/key with the path to the private key file you generated in step 5, <username> with the username you created in step 2, and <aws-vm-ip-address> with the IP address of the AWS Ubuntu VM.

Optionally, you can configure the SSH server on the AWS Ubuntu VM to disable root login and password authentication, and only allow SSH access using public key authentication. To do this, edit the /etc/ssh/sshd_config file and set the following options:

yaml
Copy code
PermitRootLogin no
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM no
PubkeyAuthentication yes
Save the file and restart the SSH server using the following command:

Copy code
sudo systemctl restart sshd
This will increase the security of your SSH access to the AWS Ubuntu VM.
