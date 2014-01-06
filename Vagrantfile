Vagrant.configure('2') do |config|
  config.vm.hostname              = ENV['DOCKER_VM_NAME']  # 好きなhostnameに変更

  config.vm.provider :digital_ocean do |provider, override|
    provider.client_id            = ENV['DIGITALOCEAN_CLIENT_ID'] # https://cloud.digitalocean.com/api_access で取得したclient_idを指定
    provider.api_key              = ENV['DIGITALOCEAN_API_KEY']   # https://cloud.digitalocean.com/api_access で取得したapi_keyを指定
    provider.ssh_key_name         = ENV['DIGITALOCEAN_SSH_KEYS']  # https://cloud.digitalocean.com/ssh_keys   で設定したSSH鍵名を指定

    override.ssh.private_key_path = '~/.ssh/digitalocean_id_rsa'
    override.vm.box               = 'digital_ocean'
    override.vm.box_url           = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.image                = 'CentOS 6.4 x64'
    provider.region               = 'New York 1'
    provider.size                 = '1GB'
    provider.ca_path              = '/usr/local/opt/curl-ca-bundle/share/ca-bundle.crt'
  end
  
  config.vm.provider :virtualbox do |provider|
    config.vm.box = "centos6.4"
    config.vm.box_url = "http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20130731.box"
    provider.memory = 512
  end

  config.vm.provision :shell, :inline => <<-EOT
    rpm -Uvh http://ftp-srv2.kddilabs.jp/Linux/distributions/fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm
    yum -y upgrade
    yum -y install docker-io
    chkconfig docker on
    service docker start
  EOT

end
