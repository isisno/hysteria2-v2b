安装docker，docker compose
curl -fsSL https://get.docker.com | bash -s docker
sudo systemctl start docker
sudo systemctl enable docker
docker --version
docker-compose –version

下载并修改配置文件,包括前端信息和后端域名
cd /etc
git clone https://github.com/isisno/hysteria.git

配置ssl证书 #使用acme配置证书要暂用80端口，可以解除占用80端口的程序之后再重启：
yum install -y openssl curl socat
curl https://get.acme.sh | sh -s email=office123@outlook.com
~/.acme.sh/acme.sh --upgrade --auto-upgrade
#可选：切换申请letsencrypt的证书
~/.acme.sh/acme.sh --set-default-ca --server letsencrypt
黄色部分换成你自己的后端vps绑定域名
~/.acme.sh/acme.sh --issue -d us001.istimeall.top --standalone
移动证书位置：
~/.acme.sh/acme.sh --install-cert -d us001.istimeall.top --key-file /etc/hysteria/us001.istimeall.top.key
~/.acme.sh/acme.sh --install-cert -d us001.istimeall.top --fullchain-file /etc/hysteria/us001.istimeall.top.crt

docker compose up -d
docker logs -f hysteria
