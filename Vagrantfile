Vagrant.configure('2') do |config|
  config.vm.hostname              = ENV['DOCKER_VM_NAME']  # 好きなhostnameに変更

  config.vm.provider :digital_ocean do |provider, override|
    provider.client_id            = ENV['DIGITALOCEAN_CLIENT_ID'] # https://cloud.digitalocean.com/api_access で取得したclient_idを指定
    provider.api_key              = ENV['DIGITALOCEAN_API_KEY']   # https://cloud.digitalocean.com/api_access で取得したapi_keyを指定
    provider.ssh_key_name         = ENV['DIGITALOCEAN_SSH_KEYS']  # https://cloud.digitalocean.com/ssh_keys   で設定したSSH鍵名を指定

    override.ssh.private_key_path = '~/.ssh/digitalocean_id_rsa'
    override.vm.box               = 'digital_ocean'
    override.vm.box_url           = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.image                = 'Ubuntu 13.04 x64'
    provider.region               = 'New York 1'
    provider.size                 = '1GB'
    provider.ca_path              = '/usr/local/opt/curl-ca-bundle/share/ca-bundle.crt'
  end
  
  config.vm.provider :virtualbox do |provider|
    config.vm.box = "Ubuntu 13.04 x64"
    config.vm.box_url = "http://goo.gl/ceHWg"
    provider.memory = 512
  end

  config.vm.provision :shell, :inline => <<-EOT
    sudo aptitude update
	sudo aptitude -y upgrade
	sudo aptitude install linux-image-extra-`uname -r`
	sudo sh -c "wget -qO- https://get.docker.io/gpg | apt-key add -"
	sudo sh -c "echo deb http://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
	sudo aptitude update
	sudo aptitude -y install lxc-docker git curl
	sudo docker -d &
  EOT

end
