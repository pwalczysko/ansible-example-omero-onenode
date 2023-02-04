Vagrant.configure("2") do |config|

    config.vm.define "server2004" do |server2004|
        server2004.vm.box = "ubuntu/focal64"
        server2004.vm.network "private_network", ip: "192.168.56.101", :name => 'vboxnet0', :adapter => 2
        server2004.vm.network "forwarded_port", guest: 4063, host: 4063, auto_correct: true
        server2004.vm.network "forwarded_port", guest: 4064, host: 4064, auto_correct: true
		server2004.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
		server2004.vm.network "forwarded_port", guest: 443, host: 8443, auto_correct: true

        server2004.vm.provider "virtualbox" do |vb|
            vb.name = "server2004"
            vb.memory = "20048"
            vb.cpus = "2"
        end
    end

	config.vm.provision "shell", inline: <<-SHELL
	  sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
	  echo 'MaxAuthTries 100' >> /etc/ssh/sshd_config    
	  systemctl restart sshd.service
          apt-get update && apt-get install -y sudo bash ca-certificates iproute2 python-apt aptitude python3.8 python3.8 python3-distutils curl libpq-dev build-essential python3.8-dev && apt-get clean
	SHELL
end
