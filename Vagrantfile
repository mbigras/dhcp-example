Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"
  config.ssh.insert_key = false

  config.vm.define "foo" do |t|
    t.vm.hostname = "foo"
    t.vm.network "private_network", ip: "192.168.50.2"
  end

  config.vm.define "bar" do |t|
    t.vm.hostname = "bar"
    t.vm.network "private_network", ip: "192.168.50.4", auto_config: false, mac: "080027000001"
  end

  config.vm.define "baz" do |t|
    t.vm.hostname = "baz"
    t.vm.network "private_network", ip: "192.168.50.4", auto_config: false, mac: "080027000002"
  end
end
