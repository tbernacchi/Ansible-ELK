# -*- mode: ruby -*-
# # vi: set ft=ruby :

$alias = <<SCRIPT
#!/bin/bash
cat > ~root.bashrc <<EOF
# .bashrc
# User specific aliases and functions

alias rm='rm'
alias cp='cp'
alias mv='mv'
alias ll='ls -lthr --color=auto'

# Source global definitions
 if [ -f /etc/bashrc ]; then
  . /etc/bashrc
 fi
EOF
SCRIPT

##Disable selinux, iptables e enable NTP
$node_script = <<SCRIPT
#!/bin/bash

Disable selinux:
sed -i 's/^\(SELINUX\s*=\s*\).*$/\1disabled/' /etc/selinux/config

##Setup NTP:
cp -pr /etc/localtime /etc/localtime.bkp
ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

yum install -y ntp ntpdate
systemctl enable ntpd

cat > /etc/ntpd.conf <<EOF
driftfile /var/lib/ntp/drift
restrict default kod nomodify notrap nopeer noquery
restrict -6 default kod nomodify notrap nopeer noquery
restrict 127.0.0.1
restrict -6 ::1
server a.st1.ntp.br
server b.st1.ntp.br
server c.st1.ntp.br
server d.st1.ntp.br
server a.ntp.br
server b.ntp.br
server c.ntp.br
server gos.ntp.br
includefile /etc/ntp/crypto/pw
keys /etc/ntp/keys
EOF

ntpdate -b -v a.st1.ntp.br
systemctl start ntpd

##Disable Firewall:
yum remove --purge firewalld -y
iptables -F
systemctl stop iptables
systemctl disable iptables
SCRIPT

##HOSTS
$host = <<SCRIPT
#!/bin/bash
cat > /etc/hosts <<EOF
127.0.0.1 localhost
192.168.33.100 standalone01
192.168.33.101 node01
192.168.33.102 node02
EOF
SCRIPT

##Vagrant
Vagrant.configure("2") do |config|

##Box
config.vm.box = "bento/centos-7"

 config.vm.define :standalone01 do |standalone01|
 standalone01.vm.provider :virtualbox do |v|
   v.name = "standalone01"
   v.cpus = 2
   v.customize ["modifyvm", :id, "--memory", "2048"]
 end
 standalone01.vm.network :private_network, ip: "192.168.33.100"
 standalone01.vm.hostname = "standalone01"
 standalone01.vm.provision :shell, :inline => $alias
 standalone01.vm.provision :shell, :inline => $host
 standalone01.vm.provision :hostmanager
 end

 config.vm.define :node01 do |node01|
 node01.vm.provider :virtualbox do |v|
   v.name = "node01"
   v.cpus = 2
   v.customize ["modifyvm", :id, "--memory", "1024"]
 end
 node01.vm.network :private_network, ip: "192.168.33.101"
 node01.vm.hostname = "node01"
 node01.vm.provision :shell, :inline => $alias
 node01.vm.provision :shell, :inline => $host
 node01.vm.provision :hostmanager
 end

# config.vm.define :node02 do |node02|
# node02.vm.provider :virtualbox do |v|
#   v.name = "node02"
#   v.cpus = 2
#   v.customize ["modifyvm", :id, "--memory", "1024"]
# end
# node02.vm.network :private_network, ip: "192.168.33.102"
# node02.vm.hostname = "node02"
# node02.vm.provision :shell, :inline => $alias
# node02.vm.provision :shell, :inline => $host
# node02.vm.provision :hostmanager
# end
#
end
