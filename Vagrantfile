Vagrant.configure('2') do |config|

  config.vm.box = 'puppetlabs/centos-7.0-64-puppet'
  config.ssh.forward_agent = true

  config.vm.provider 'virtualbox' do |vb|
    vb.customize ['modifyvm', :id, '--memory', '1024']
  end

  config.vm.define 'app', primary: true do |app|
    app.vm.provision :shell, inline: '/bin/bash /vagrant/scripts/vagrant-app-bootstrap app'
    app.vm.network 'forwarded_port', guest: 80, host: 8081
    app.vm.network 'forwarded_port', guest: 8080, host: 8082
    app.vm.network 'private_network', ip: '10.133.133.11'
  end

  config.vm.define 'es1' do |es|
    es.vm.provision :shell, inline: '/bin/bash /vagrant/scripts/vagrant-es-bootstrap es1'
    es.vm.network 'forwarded_port', guest: 9200, host: 9201
    es.vm.network 'forwarded_port', guest: 9300, host: 9301
    es.vm.network 'private_network', ip: '10.133.133.22'
  end

  config.vm.define 'es2' do |es|
    es.vm.provision :shell, inline: '/bin/bash /vagrant/scripts/vagrant-es-bootstrap es2'
    es.vm.network 'forwarded_port', guest: 9200, host: 9202
    es.vm.network 'forwarded_port', guest: 9300, host: 9302
    es.vm.network 'private_network', ip: '10.133.133.33'
  end

end