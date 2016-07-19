VAGRANTFILE_API_VERSION = "2"
box      = 'ubuntu/trusty64'
url      = 'https://atlas.hashicorp.com/ubuntu/boxes/trusty64'
hostname = 'jenkins'
ip       = '192.168.5.99'
ram      = '1024'

Vagrant::Config.run do |config|
  config.vm.box = box
  config.vm.box_url = url
  config.vm.host_name = hostname
  config.vm.network :hostonly, ip 

  config.vm.customize [
    'modifyvm', :id,
    '--name', hostname,
    '--memory', ram
  ]
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.network "forwarded_port", guest: 8080, host: 9090
  config.vm.network "forwarded_port", guest: 7272, host: 8000
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "jenkins.yml"
  end
end


