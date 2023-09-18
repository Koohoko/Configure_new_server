
## Cron
`sudo apt install cron`; `sudo systemctl enable cron`

## install tools
`sudo apt install wget git curl vim tmux -y`

## install zsh
```
sudo apt update
sudo apt install zsh -y
chsh -s $(which zsh)
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## Enable plug-ins
### powerlevel 10k
`git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k`
### auto suggestions
`git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`
### zsh-syntax-highlighting
`git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting`
### Zsh-z
`git clone https://github.com/agkozak/zsh-z $ZSH_CUSTOM/plugins/zsh-z`
### edit config
```
sudo nano ~/.zshrc
# ZSH_THEME="powerlevel10k/powerlevel10k"
# plugins=(git zsh-autosuggestions zsh-syntax-highlighting zsh-z)
source ~/.zshrc
```

### code server
```shell
curl -fsSL https://code-server.dev/install.sh | sh
sudo systemctl enable --now code-server@$USER
nano ~/.config/code-server/config.yaml
```

### cloudflared
- Follow this: https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/install-and-setup/tunnel-guide/local/
```
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb && sudo dpkg -i cloudflared-linux-amd64.deb
cloudflared tunnel login
cloudflared tunnel create R6625_container
cloudflared tunnel list

nano ~/.cloudflared/config.yml

#tunnel: <Tunnel-UUID>
#credentials-file: /root/.cloudflared/<Tunnel-UUID>.json
#ingress:
#  - hostname: ssh_R6625_container.guhaogao.com
#    service: ssh://localhost:22
#  - hostname: code_R6625_container.guhaogao.com
#    service: http://localhost:8080
#  - service: http_status:404

cloudflared tunnel route dns R6625_container ssh_R6625_container.guhaogao.com # new CNAME
cloudflared tunnel route dns R6625_container code_R6625_container.guhaogao.com # new CNAME
cloudflared tunnel run R6625_container

# Don't forget to create zero-trust access application !!!

# Auto start
sudo cloudflared service install
sudo cp /home/hggu/.cloudflared/config.yml /etc/cloudflared/config.yml
sudo cloudflared service install
sudo systemctl start cloudflared
sudo systemctl restart cloudflared

```


