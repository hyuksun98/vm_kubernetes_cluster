Vagrant.configure("2") do |config|
  config.vm.define "control1" do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.hostname = "control1"
    config.vm.network "private_network", ip: "192.168.56.101"
    config.disksize.size = "100GB"
    config.vm.provider "virtualbox" do |vb|
      vb.name = "control1"
      vb.cpus = 6
      vb.memory = 12288
    end
  end

  config.vm.define "worker22" do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.hostname = "worker22"
    config.vm.network "private_network", ip: "192.168.56.102"
    config.disksize.size = "100GB"
    config.vm.provider "virtualbox" do |vb|
      vb.name = "worker22"
      vb.cpus = 6
      vb.memory = 12288
    end
  end

  # Hostmanager plugin
  config.hostmanager.enabled = true
  config.hostmanager.manage_guest = true

  # Enable SSH Password Authentication
  config.vm.provision "shell", inline: <<-SHELL
    sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/g' /etc/ssh/sshd_config
    sed -i 's/archive.ubuntu.com/ftp.daum.net/g' /etc/apt/sources.list
    sed -i 's/security.ubuntu.com/ftp.daum.net/g' /etc/apt/sources.list
    systemctl restart ssh
    systemctl start systemd-timesyncd
    timedatectl set-timezone UTC
  SHELL
end
