Vagrant.configure("2") do |config|
  # Especificar la box base
  config.vm.box = "ubuntu/focal64"
  config.vm.box_version = "20220131.1.0"

  # Configuración de red: cambiar a IP estática para evitar conflictos
  config.vm.network "private_network", ip: "192.168.56.10"

  # Desactivar la carpeta compartida predeterminada para evitar conflictos
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Configuración de la máquina virtual
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"      # Asigna 512 MB de RAM
    vb.cpus = 1            # Asigna 1 CPU
    vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update -y
    sudo apt-get install -y apache2
  SHELL

  config.vm.synced_folder "./src", "/var/www/html", type: "virtualbox"
end
