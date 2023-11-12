### 基于centos7系统
### 安装docker，docker compose
`curl -fsSL https://get.docker.com | bash -s docker`  
`sudo systemctl start docker`  
`sudo systemctl enable docker`  
`docker --version`  
`docker compose version`  

### 下载并修改配置文件docker-compose.yml,server.yaml,包括前端信息和后端域名  
`cd /etc`  
`git clone https://github.com/isisno/hysteria.git`  
`cd /etc/hysteria`  

### 配置ssl证书，使用acme配置证书要暂用80端口，可以解除占用80端口的程序之后再重启：  
`yum install -y openssl curl socat`  
`curl https://get.acme.sh | sh -s email=office123@outlook.com`  
`~/.acme.sh/acme.sh --upgrade --auto-upgrade`  
可选：切换申请letsencrypt的证书  
`~/.acme.sh/acme.sh --set-default-ca --server letsencrypt`  
黄色部分换成你自己的后端vps绑定域名  
`~/.acme.sh/acme.sh --issue -d example.com --standalone`  
移动证书位置：  
`~/.acme.sh/acme.sh --install-cert -d example.com --key-file /etc/hysteria/example.com.key`  
`~/.acme.sh/acme.sh --install-cert -d example.com --fullchain-file /etc/hysteria/example.com.crt`  

### 启动docker compose  
`docker compose up -d`  
`docker logs -f hysteria`  
