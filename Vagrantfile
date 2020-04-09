# -*- mode: ruby -*-
# vi: set ft=ruby :

module OS
  def OS.windows?
    Vagrant::Util::Platform.windows?
  end
end

VAGRANTFILE_API_VERSION = "2"

def install_plugin(plugin)
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

# 必要なプラグインを指定
install_plugin('vagrant-hostsupdater')
install_plugin('vagrant-vbguest')

Vagrant.configure(2) do |config|
  config.vm.box = "bento/centos-7.2"
  # ssl接続時証明書を検証しない
  config.vm.box_download_insecure = true

  config.vm.define "vue" do |machine|
    # ホストPCとゲストPCのネットワークを構築
    machine.vm.network "private_network", ip: "192.168.33.100"

    # ホストPCにポートも転送
    machine.vm.network "forwarded_port", guest: 80, host: 8000
    machine.vm.network "forwarded_port", guest: 443, host: 8443

    # ホストPCのこのフォルダをマウント
    machine.vm.synced_folder "./vue", "/vagrant", create: true, mount_options: ['dmode=777','fmode=777']

    # メモリサイズ
    machine.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
    end

    # windowsの方は管理者権限でないと動きません
    machine.vm.hostname = "vm.ofstest.com"

    machine.vbguest.auto_update = false

    if OS.windows?
      machine.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
      end
    else
      machine.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
      end
    end
  end

  config.vm.define "api" do |machine|
    # ホストPCとゲストPCのネットワークを構築
    machine.vm.network "private_network", ip: "192.168.33.101"

    # ホストPCにポートも転送
    machine.vm.network "forwarded_port", guest: 80, host: 8001
    machine.vm.network "forwarded_port", guest: 443, host: 8444

    # ホストPCのこのフォルダをマウント
    machine.vm.synced_folder "./api", "/vagrant", create: true, mount_options: ['dmode=777','fmode=777']

    # メモリサイズ
    machine.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
    end

    # windowsの方は管理者権限でないと動きません
    machine.vm.hostname = "api.ofstest.com"

    machine.vbguest.auto_update = false

    if OS.windows?
      machine.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible/playbook-api.yml"
      end
    else
      machine.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook-api.yml"
      end
    end
  end
end