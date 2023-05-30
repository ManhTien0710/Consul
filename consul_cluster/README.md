# install consul: 3 node consul-server & 1 node consul-agent
```bash
- server1: 172.16.10.77
- server2: 172.16.10.78
- server3: 172.16.10.79
- Server4-Agent: 172.16.10.80
```
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
# Config consul-server on 3 node consul-server
```bash
vi /etc/consul.d/config.json
vi /usr/lib/systemd/system/consul.service
```
# config consul-agent on 1 node consul-agent
```bash
vi /etc/consul.d/config.json
vi /usr/lib/systemd/system/consul.service
```
# validate config
```bash
consul validate /etc/consul.d/config.json
```
# note
```bash
- `node_name` : Tên server join vào cluster.
- `data_dir`: thư mục chứa dữ liệu hoạt động của consul
- `ui_config`: kích hoạt giao diện quản lý
- `client_addr`: địa chỉ IP mà consul sẽ listen interface.
- `server`: mode server(true)
- `ports`: port lắng nghe dịch vụ
- `start_join`: cụm địa chỉ IP server cluster
- `retry_join`: Join vào các danh sách các máy chủ trong cụm cluster nếu start_join thất bại.
- `bootstrap_expect`: số lượng consul server cần có để chạy cluster
- `bind_addr` : IP của node
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
# using keepalived for HA 2 consul agent.