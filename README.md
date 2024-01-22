# vagrant-webserver

## Getting started
In this tutorial, you will serve local files using a webserver on a guest machine.


## Installation
- VirtualBox [Download here:](https://www.virtualbox.org/wiki/Downloads)
- Vagrant [Download here:](https://developer.hashicorp.com/vagrant/downloads)

## Deploy the webserver
```
vagrant up
```

## Verify deployment
After Vagrant completes provisioning, the web server will be active. You cannot see the website from your own browser yet, but you can verify that the provisioning works by loading a file from within the machine.

SSH into the guest machine.
```
vagrant ssh
```
Now get the HTML file that was created during provisioning.

```
vagrant@vagrant:~ wget -qO- 127.0.0.1
<!DOCTYPE html>
<html>
  <body>
    <h1>....<\h1>
  </body>
</html>
```

## Configure the Network
### Configure port forwarding
To set up a forwarded port so you can access Apache on your guest, add the config.vm.network parameter to your Vagrantfile. Below is the full file with port forwarding.
```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.provision :shell, path: "bootstrap.sh"
  config.vm.network :forwarded_port, guest: 80, host: 4567
end
```
Reload so that these changes can take effect.

```
vagrant reload
```
### Access the served files
Once the machine has loaded, you can access http://127.0.0.1:4567 in your browser. You will find a web page that is being served from the guest virtual machine.

## Authors and acknowledgment
Show your appreciation to those who have contributed to the project.

## License
For open source projects, say how it is licensed.
