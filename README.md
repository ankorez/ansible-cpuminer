# ansible-cpuminer-rpi

For easy deploy cpuminer on raspberry pi

## Install Ansible
Add Ansible repo to /etc/apt/sources.list

>    deb http://ppa.launchpad.net/ansible/ansible/ubuntu bionic main

Run installation

    sudo apt update && sudo apt upgrade -y

Install ansible galaxy collection

    ansible-galaxy collection install community.general

## Add SSH Key on each Raspberry

    ssh-copy-id pi@192.168.x.x

## Edit inventory

    sudo nano inventory
Add IPs of raspberry pi hosts on which we want deploy cpu-miner

## Edit playbook.yaml

    sudo nano playbook.yaml
Change the line in playbook with your informations from minergate

    - name: Add to crontab
      ansible.builtin.cron:
        name: "cpuminer"
        special_time: reboot
        job: "/home/pi/cpuminer-multi/cpuminer -a cryptonight -o stratum+tcp://xmr.pool.minergate.com:45700 -u monemail@gmail.com"

## Run playbook

    ansible-playbook -i inventory playbook.yaml
