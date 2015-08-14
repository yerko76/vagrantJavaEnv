# encoding: utf-8
# This file originally created at http://rove.io/a55ee3b5ca0c4652ab546d78f86729a7

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "opscode-ubuntu-12.04_chef-11.4.0"
  config.vm.box_url = "https://opscode-vm-bento.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_chef-11.4.0.box"
  config.ssh.forward_agent = true
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.synced_folder "C:/supplychain-box", "/home/vagrant"

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe :apt
    chef.cookbooks_path = ["cookbooks"]
    chef.add_recipe 'rvm::vagrant'
    chef.add_recipe 'rvm::system'
    chef.add_recipe 'nodejs'
    chef.add_recipe 'git'
    chef.add_recipe 'vim'
    chef.add_recipe 'subversion'
    chef.add_recipe 'tmux'
    chef.add_recipe 'java'
    chef.add_recipe 'gradle'
    chef.add_recipe 'mongodb'
    chef.json = {
      :git        => {
        :prefix => "/usr/local"
      },
      :vim        => {
        :extra_packages => [
          "vim-rails"
        ]
      },
      :gradle => {
            :version => "2.4"
      },
      :java => {
        :jdk_version => "7",
        :oracle => {
          "accept_oracle_download_terms" => true
        }
      },
      :subversion => {
        :repo_dir    => "/srv/svn",
        :repo_name   => "repo",
        :server_name => "svn",
        :user        => "subversion",
        :password    => "subversion"
      },
      :mongodb => {
        :dbpath  => "/var/lib/mongodb",
        :logpath => "/var/log/mongodb",
        :port    => "27017"
      }
    }
  end

  config.vm.provision "shell" do |s|
    s.inline = <<-EOS
       curl http://j.mp/spf13-vim3 -L -o - | sh
     EOS
  end

end
