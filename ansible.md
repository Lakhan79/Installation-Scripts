#!/bin/bash

# This script installs ansible on ubuntu on AWS

# Run this script as root or with sudo privileges

# Update the system
apt update -y
apt upgrade -y

# Install python3 and pip3
apt install python3 python3-pip -y

# Install ansible using pip3
pip3 install ansible

# Create an ansible user and add it to the sudo group
useradd -m -s /bin/bash ansible
usermod -aG sudo ansible

# Generate an ssh key pair for the ansible user and copy the public key to the authorized_keys file
su - ansible -c "ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa -q -N ''"
su - ansible -c "cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys"

# Enable passwordless sudo for the ansible user
echo "ansible ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/ansible > /dev/null

# Test the ansible installation by running the ping module on localhost
su - ansible -c "ansible localhost -m ping"
