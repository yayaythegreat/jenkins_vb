Vagrant.configure("2") do |config|
  config.vm.define "my_centos_box" do |c|
    c.vm.box = "centos/7"
    # c.vbguest.installer_options = { allow_kernel_upgrade: true }
    c.vm.network "public_network"
    config.vm.synced_folder ".", "/vagrant_data"
    c.vm.provision "shell", inline: <<-SHELL
      sudo yum install -y yum-utils
      sudo yum-config-manager  --add-repo https://download.docker.com/linux/centos/docker-ce.repo
      sudo yum -y install docker-ce docker-ce-cli containerd.io
      sudo systemctl start docker
      sudo systemctl enable docker
      sleep 30
      # docker run  --name jenkins-docker   --rm   --detach   --privileged   --network jenkins  --network-alias docker  --env DOCKER_TLS_CERTDIR=/certs  --volume jenkins-docker-certs:/certs/client   --volume jenkins-data:/var/jenkins_home   --publish 2376:2376   docker:dind   --storage-driver overlay2
      # cd /vagrant_data/ && docker build -t jenkins_blueocean
    SHELL
  end

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
end
