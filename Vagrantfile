# Vagrantfile for Yolo App Configuration Management Project
# Stage 1: Ansible Instrumentation

Vagrant.configure("2") do |config|
  # Use Jeff Geerling's Ubuntu 20.04 image
  config.vm.box = "geerlingguy/ubuntu2004"

  # Set a friendly hostname
  config.vm.hostname = "yolo-app"

  # Forward port 3000 (React frontend)
  config.vm.network "forwarded_port", guest: 3000, host: 3000

  # Provisioner: Ansible playbook that will handle Docker setup and deployment
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yaml"
  end

  # Provider: VirtualBox settings
  config.vm.provider "virtualbox" do |vb|
    vb.name = "yolo-app"
   
  end
end
