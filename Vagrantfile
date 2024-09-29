Vagrant.configure("2") do |config|
  config.vm.box = "kalilinux/rolling"
  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.network "public_network", ip: "192.168.1.150"

  # Set RAM and CPU
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8192" # 8GB RAM
    vb.cpus = 2
    vb.gui = true
    vb.customize ["modifyvm", :id, "--vram", "128"] # Increase video RAM for GUI
  end

  # Provision to install Kali Linux desktop environment and Apache HTTP Server
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get upgrade -y
    sudo apt-get install -y kali-desktop-xfce
    sudo apt-get install -y apache2
    sudo systemctl start apache2
    sudo systemctl enable apache2
    sudo apt-get install -y kali-linux-default
  SHELL
end