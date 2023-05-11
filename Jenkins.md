#!/bin/bash
# This script installs jenkins on ubuntu on AWS
# Run this script as root or with sudo privileges
 
# Update the system
apt update -y
apt upgrade -y
 
# Install openjdk-17-jre
apt install openjdk-17-jre -y
 
# Add jenkins repository key and source list
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
 
# Update the system again
sudo apt-get update -y
 
# Install jenkins
sudo apt-get install -y jenkins
 
# Start and enable jenkins service
sudo systemctl start jenkins
sudo systemctl enable jenkins
