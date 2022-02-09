Vagrant.configure("2") do |config|
  servers=[
      {
        :hostname => "prometheus-server",
        :box => "bento/ubuntu-18.04",
        :ip => "192.168.56.101",
        :ram => 4096,
        :cpu => 1,
        :ssh_port => '2200'
      },
      {
        :hostname => "server1",
        :box => "bento/ubuntu-18.04",
        :ip => "192.168.56.102",
        :ram => 1024,
        :cpu => 1,
        :ssh_port => '2201'
      },
      {
        :hostname => "server2",
        :box => "bento/ubuntu-18.04",
        :ip => "192.168.56.103",
        :ram => 1024,
        :cpu => 1,
        :ssh_port => '2202'
      }
    ]

  servers.each do |machine|
      config.vm.define machine[:hostname] do |node|
          node.vm.box = machine[:box]
          node.vm.hostname = machine[:hostname]
          node.vm.network :private_network, ip: machine[:ip]
          node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
          node.vm.provider :virtualbox do |vb|
              vb.memory = machine[:ram]
              vb.cpus = machine[:cpu]
          end
          node.ssh.forward_agent = true
          node.vm.provision :shell, inline: <<-SHELL
            sudo apt-get update -y
            curl -fsSL https://get.docker.com -o get-docker.sh
            sudo sh get-docker.sh
            sudo groupadd docker
            sudo usermod -aG docker $USER
            sudo chmod 666 /var/run/docker.sock
            sudo apt install -y docker-compose
          SHELL
      end
  end
end