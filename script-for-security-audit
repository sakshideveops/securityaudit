#!/bin/bash

# Security audit and hardening script for Linux servers

# Function to check for open ports and unnecessary services
audit_open_ports() {
    echo "Auditing open ports and services..."
    netstat -tulpn | grep LISTEN
    echo "Ensure only necessary services are running."
}

# Function to review system logs for unauthorized access
audit_logs() {
    echo "Reviewing system logs for unauthorized access..."
    grep -i "failed" /var/log/auth.log
}

# Function to verify user accounts and password policies
audit_users() {
    echo "Verifying user accounts and password policies..."
    cat /etc/passwd | awk -F: '$3 < 1000 { print $1 }'
    grep PASS_MAX_DAYS /etc/login.defs
}

# Function to check for outdated packages and security patches
audit_packages() {
    echo "Checking for outdated packages and security patches..."
    sudo apt update && sudo apt list --upgradable
}

# Function to verify firewall settings and configurations
audit_firewall() {
    echo "Verifying firewall settings..."
    sudo ufw status verbose
}

# Function to check IPv4 and IPv6 configurations
audit_ip_config() {
    echo "Checking IPv4 and IPv6 configurations..."
    ip -4 a
    ip -6 a
}

# Function to identify public vs private IP addresses
identify_ip_type() {
    echo "Identifying public vs private IP addresses..."
    ip addr | grep inet
}

# Function to disable unused services
harden_disable_services() {
    echo "Disabling unused services..."
    sudo systemctl disable <service_name>
}

# Function to enforce strong password policies
harden_password_policies() {
    echo "Enforcing strong password policies..."
    sudo sed -i 's/PASS_MAX_DAYS.*/PASS_MAX_DAYS   90/' /etc/login.defs
    sudo sed -i 's/PASS_MIN_DAYS.*/PASS_MIN_DAYS   10/' /etc/login.defs
}

# Function to set up automatic updates for security patches
harden_auto_updates() {
    echo "Setting up automatic updates for security patches..."
    sudo apt install unattended-upgrades
    sudo dpkg-reconfigure --priority=low unattended-upgrades
}

# Function to configure firewalls and IP tables
harden_firewall() {
    echo "Configuring firewalls..."
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    sudo ufw enable
}

# Function to implement SSH hardening
harden_ssh() {
    echo "Implementing SSH hardening..."
    sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
    sudo systemctl restart sshd
}

# Function to disable root login via SSH
disable_root_ssh() {
    echo "Disabling root login via SSH..."
    sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
    sudo systemctl restart sshd
}

# Function to restrict access to sensitive files and directories
restrict_access() {
    echo "Restricting access to sensitive files and directories..."
    sudo chmod -R go-rwx /root/
}

# Main function to run all audits and hardening steps
main() {
    audit_open_ports
    audit_logs
    audit_users
    audit_packages
    audit_firewall
    audit_ip_config
    identify_ip_type
    harden_disable_services
    harden_password_policies
    harden_auto_updates
    harden_firewall
    harden_ssh
    disable_root_ssh
    restrict_access
}

# Execute the main function
main
