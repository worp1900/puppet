# Puppet

Just a collection of memories about puppet and local experiments.

## Setup

### Install Master Ubuntu 20.04

    sudo hostnamectl set-hostname puppetmaster

    # Add master and agents to /etc/hosts

    wget https://apt.puppet.com/puppet7-release-focal.deb \
    && sudo dpkg -i puppet7-release-focal.deb \
    && sudo apt update \
    && sudo apt upgrade -y 

    sudo apt install -y puppetserver \
    && sudo apt autoremove -y \
    && sudo systemctl enable puppetserver \
    && sudo systemctl start puppetserver \
    && sudo systemctl start puppet

    sudo apt install -y puppetdb \
    && sudo systemctl enable puppetdb \
    && sudo systemctl start puppetdb

### Install Slave Ubuntu 20.04

    sudo hostnamectl set-hostname puppetagent

    # Add master and agents to /etc/hosts

    wget https://apt.puppet.com/puppet7-release-focal.deb \
    && sudo dpkg -i puppet7-release-focal.deb \
    && sudo apt update \
    && sudo apt upgrade -y \
    && sudo apt install -y puppet-agent

    # New from here:

    # Make sure the service runs
    sudo /opt/puppetlabs/bin/puppet resource service puppet ensure=running enable=true

    # Adjust path
    source /etc/profile.d/puppet-agent.sh

    # Configure puppet master
    sudo puppet config set server puppetmaster --section main