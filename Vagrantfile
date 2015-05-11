Vagrant.configure(2) do |config|
  config.vm.box = "debian/jessie64"

  config.vm.hostname = "vpn.techpunch.com"

  config.vm.synced_folder "puppet", "/etc/puppet"

  config.vm.synced_folder "openvpn", "/root/openvpn"

  config.vm.provision "shell",
    inline: "
        FQDN=`hostname --fqdn`;
        mkdir -p /etc/openvpn/keys;
        cp /root/openvpn/key-store/ca.crt /etc/openvpn/keys/;
        cp /root/openvpn/key-store/$FQDN.crt /etc/openvpn/keys/;
        cp /root/openvpn/key-store/$FQDN.key /etc/openvpn/keys/;
        cp /root/openvpn/key-store/dh2048.pem /etc/openvpn/keys/;
        puppet apply /etc/puppet/environments/production/manifests/site.pp --confdir=/etc/puppet/ --environment=production --environmentpath=/etc/puppet/environments/
    "
end
