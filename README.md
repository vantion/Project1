Project 1
cd ~
mkdir utrains-project
cd utrains-project
mkdir project1
cd project1
code Vagrantfile
paste below code into the Vagrantfile and then save.

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # load de centos7 box from vagrant cloud
    config.vm.box = "utrains/centos7"
    config.vm.box_version = "3.0"
    config.vm.network "private_network", ip: "192.168.56.30"
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      #vb.name = "centos-project1"
      vb.cpus = 2
    end
    #change the value of the SSH configuration file, then restart the ssh service
    config.vm.provision "shell", inline: <<-SHELL
     sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
     sudo systemctl restart sshd
    SHELL
  end


vagrant up
vagrant ssh 

What is Apache?
Apache is a free and open-source software that allows users to deploy their websites on the internet. It is one of the oldest and most reliable web server software maintained by the Apache Software Foundation, with the first version released in 1995.There are other webserver softwares available like tomcat, iis, nginx and more.
To install apache, we need a Centos/redhat machine and we can run below commands:
1- # yum install httpd -y ( httpd is the package name for apache on centos/redhat system)
2- # systemctl status httpd ( to check the httpd daemon/service)
3- # systemctl start httpd (to start the daemon)
4- # ifconfig (get the ip address and type it on the browser. you will see a default apache page.)
5- Sometimes the system has firewall enabled. In that case, we need to open port 80 on the system since apache runs on port 80:
# firewall-cmd --permanent --add-port=80/tcp
# firewall-cmd --reload
6- We can move into /var/www/html, add an index.html file to replace the default content on the browser.
# cd /var/www/html
# touch index.html
# vi index.html
<h1>This is my first personal website</h1>
:wq (to save and quit)
Then refresh the browser to see the new content.
TODO: There is a need for a webserver in your team, please follow these steps to install one.
