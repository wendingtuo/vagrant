# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "kalilinux/rolling"
  config.vm.provider "vmware_desktop" do |v|
    current_dir = File.basename(Dir.getwd)
    v.vmx["displayname"] = current_dir
    v.gui = true
    v.functional_hgfs = true
    v.vmx["memsize"] = "8192"
    v.vmx["numvcpus"] = "4"
    v.vmx["usb.generic.allowHID"] = true
    v.vmx["mouse.vusb.enable"] = true
    v.vmx["mouse.vusb.useBasicMouse"] = false
    v.vmx["ulm.disableMitigations"] = true
    v.vmx["isolation.tools.dnd.disable"] = true
  config.vm.synced_folder ".", "/home/vagrant/vmshare", owner: "vagrant", group: "vagrant"
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y nix
    bash -c "$(curl -fsSL https://get.jetify.com/devbox)" -y -f
    #/usr/bin/vmhgfs-fuse .host:/ /home/blake/share -o subtype=vmhgfs-fuse,allow_other 
  SHELL
end
