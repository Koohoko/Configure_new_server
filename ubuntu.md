
## Cron
`sudo apt install cron`; `sudo systemctl enable cron`

## install tools
`sudo apt install wget git curl vim -y`

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
sudo nano ~/zshrc
# ZSH_THEME="powerlevel10k/powerlevel10k"
# plugins=(git zsh-autosuggestions zsh-syntax-highlighting zsh-z)
source ~/.zshrc
```

## cloudflared
- Follow this: https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/install-and-setup/tunnel-guide/local/
```
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb && sudo dpkg -i cloudflared-linux-amd64.deb
cloudflared tunnel login
cloudflared tunnel create <NAME>
cloudflared tunnel list

nano ~/.cloudflared/config.yml
#url: http://localhost:8000
#tunnel: <Tunnel-UUID>
#credentials-file: /root/.cloudflared/<Tunnel-UUID>.json

cloudflared tunnel route dns R6625_host lxdui.guhaogao.com # new CNAME

```

## code-server

