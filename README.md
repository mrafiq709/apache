# Apache-Tomcat-CentOS
Apache Tomcate in CentOS7

After Screenshot 10 edit VagrantFile:
-------------------------------
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.33.10"
