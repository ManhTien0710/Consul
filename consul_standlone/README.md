# install consul
```bash
sudo yum install java-11-openjdk.x86_64 -y
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo yum -y install consul
```
# open port
```bash
firewall-cmd --add-port={8300,8301,8302,8400,8500,8600}/tcp --permanent
firewall-cmd --add-port={8301,8302,8600}/udp --permanent
firewall-cmd --reload
iptables -I INPUT -p tcp --match multiport --dports 8300,8301,8302,8400,8500,8600 -j ACCEPT
iptables -I INPUT -p udp --match multiport --dports 8301,8302,8600 -j ACCEPT
```
# Config consu;
```bash
vi /etc/consul.d/config.json
vi /usr/lib/systemd/system/consul.service
```
# validate config
```bash
consul validate /etc/consul.d/config.json
```
# check status service
```bash
systemctl daemon-reload
systemctl restart consul.service
systemctl status consul.service
systemctl enable consul.service
```
# remove service 
```bash
consul services deregister -id={Your Service Id}
```
