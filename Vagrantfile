# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

  Vagrant.configure("2") do |config|

    config.vm.define "web" do |web|
    web.vm.box = "ubuntu/xenial64"
    web.vm.network "private_network", ip: "192.168.10.100"
    web.hostsupdater.aliases = ["development.local"]
    web.vm.synced_folder ".", "/home/ubuntu/app"
    web.vm.provision "shell", path: "environment/app/provision.sh", privileged: false

    end

    config.vm.define "db" do |db|
    db.vm.box = "ubuntu/xenial64"
    db.vm.hostname = 'db'
    db.vm.network "private_network", ip: "192.168.56.102"
    db.vm.synced_folder ".", "/home/ubuntu/app"
    db.vm.provision "shell", path: "environment/db/provision.sh", privileged: false

    end
end
