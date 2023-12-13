
## Cron
```
sudo apt install cron
sudo systemctl enable cron
```

## install tools
```
sudo apt install wget git curl vim tmux htop -y
```

## edit htop

```
echo "# Beware! This file is rewritten by htop when settings are changed in the interface.
# The parser is also very primitive, and not human-friendly.
fields=0 48 17 18 38 39 40 2 46 47 49 1
sort_key=46
sort_direction=-1
tree_sort_key=0
tree_sort_direction=1
hide_kernel_threads=1
hide_userland_threads=0
shadow_other_users=0
show_thread_names=0
show_program_path=1
highlight_base_name=0
highlight_megabytes=1
highlight_threads=1
highlight_changes=0
highlight_changes_delay_secs=5
find_comm_in_cmdline=1
strip_exe_from_cmdline=1
show_merged_command=0
tree_view=0
tree_view_always_by_pid=0
header_margin=1
detailed_cpu_time=0
cpu_count_from_one=0
show_cpu_usage=1
show_cpu_frequency=0
show_cpu_temperature=0
degree_fahrenheit=0
update_process_names=0
account_guest_in_cpu_meter=0
color_scheme=0
enable_mouse=1
delay=15
left_meters=LeftCPUs4 DateTime Uptime Tasks LoadAverage Hostname
left_meter_modes=1 2 2 2 2 2
right_meters=RightCPUs4 CPU Memory Swap DiskIO NetworkIO
right_meter_modes=1 1 1 1 2 2
hide_function_bar=0" > ~/.config/htop/htoprc
```

## install zsh
```
sudo apt update
sudo apt install zsh -y
chsh -s $(which zsh)
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## Enable plug-ins
### powerlevel 10k
```
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```
### auto suggestions
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
### zsh-syntax-highlighting
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
### Zsh-z
```
git clone https://github.com/agkozak/zsh-z $ZSH_CUSTOM/plugins/zsh-z
```
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

sudo mkdir /root/.cloudflared/
sudo cp /home/hggu/.cloudflared/*.json /root/.cloudflared/
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
sudo mkdir /etc/cloudflared/
sudo cp /home/hggu/.cloudflared/config.yml /etc/cloudflared/config.yml
sudo cloudflared service install
sudo systemctl start cloudflared
sudo systemctl status cloudflared
sudo systemctl restart cloudflared

```

### monitor
```
curl -LO https://github.com/ClementTsang/bottom/releases/download/0.9.6/bottom_0.9.6_amd64.deb
sudo dpkg -i bottom_0.9.6_amd64.deb
```

### R
```shell
sudo apt install r-base r-base-dev -y
pip3 install -U radian
# add to path
# export PATH=$HOME/bin:/usr/local/bin:/home/hggu/.local/bin:$PATH
sudo apt-get install -y libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev libcurl4-openssl-dev libbz2-dev liblzma-dev libssl-dev libxml2-dev libfontconfig1-dev libharfbuzz-dev libfribidi-dev # pre-requisite for installing tidyverse

```
