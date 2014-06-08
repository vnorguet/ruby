# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "base"

  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_ubuntu-14.04_chef-provisionerless.box"

  config.ssh.username = "vagrant"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #

  config.omnibus.chef_version = "11.12.8"

  config.vm.provision "chef_solo" do |chef|
    chef.custom_config_path = "Vagrantfile.chef"

    chef.cookbooks_path = "cookbooks"
    # chef.add_recipe "base"
    chef.add_recipe "mysql::server"
    chef.add_recipe "ruby_build"
    chef.add_recipe "rbenv::user"
    chef.add_recipe "rbenv::vagrant"

    # TODO
    # chef.add_recipe "nginx"
    # chef.add_recipe "zsh"
    # chef.add_recipe "git"
    # chef.add_recipe "curl"
    # package "libmysqlclient-dev"


    # You may also specify custom JSON attributes:
    chef.json = {
      :mysql => { :server_root_password => 'foo_alpha' },
      :rbenv => {
        :user_rubies => ['2.1.2'],
        :global  => '2.1.2',
        :user_installs => [
          {
            :user    => 'vagrant',
            :global  => '2.1.2',
            :rubies  => ['2.1.2'],
            :gems    =>
            {
              '2.1.2' => [
                { :name => 'bundler' },
                { :name => 'capistrano' }
              ]
            }
          }
        ]
      }
    }
  end

end
