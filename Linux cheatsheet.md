# `Linux`

## My definitive guide to the soul of Linux commands by [Felipe Sardi](mailto:felipe.sardi@gmail.com)

# Alias

## *.bash\_aliases*

`cat > ~/.bash_aliases << EOF`  
`# Felipe Sardi (2024-10-15)`  
`alias ..='cd ..'`  
`alias ...='cd ../..'`  
`alias etc='cd /etc'`  
`alias hm='cd ~'`  
`alias mnt='cd /mnt'`  
`alias monet='cd /mnt/monet'`  
`alias media='cd /mnt/monet/media'`  
`alias mount='mount |column -t'`  
`alias ai='sudo apt -y install'`  
`alias ar='sudo apt purge'`  
`alias au='sudo apt-get update && sudo apt-get -y upgrade && sudo apt autoremove'`  
`alias adu='sudo apt dist-upgrade'`  
`alias bc='bc -l'`  
`alias blkid='blkid -o list'`  
`alias btl='sudo btrfs subvolume list .'`  
`alias chk='sudo e2fsck -p -f -C 0 /dev/'`  
`alias bchk='sudo btrfs check --repair /dev/'`  
`alias df='df -H'`  
`alias du='du -ch'`  
`alias e='emacs'`  
`alias se='sudo -E emacs'`  
`alias ealias='emacs ~/.bash_aliases && source ~/.bashrc'`  
`alias efstab='sudo -E emacs /etc/fstab'`  
`alias edeluge='sudo -E emacs /var/lib/deluged/config/core.conf'`  
`alias esamba='sudo -E emacs /etc/samba/smb.conf && sudo systemctl restart smbd nmbd'`  
`alias essh='sudo -E emacs /etc/ssh/sshd_config && sudo systemctl restart ssh'`  
`alias fgrep='fgrep --color=auto'`  
`alias egrep='egrep --color=auto'`  
`alias grep='grep --color=auto'`  
`alias agroup='sudo usermod -aG '`  
`alias h='history'`  
`alias hdspeed='dd if=/dev/zero of=hdspeedfile bs=1M count=1024 conv=fdatasync && sudo sh -c "/usr/bin/echo 3 > /proc/sys/vm/drop_caches" && dd if=hdspeedfile of=/dev/null bs=1M count=1024'`  
`alias ipscan=arp-scanner`  
`alias ipfull='nmcli device show'`  
`alias j='jobs -l'`  
`alias l='ls -CF'`  
`alias l.='ls -d .* --color=auto'`  
`alias la='ls -A'`  
`alias ll='ls -alF'`  
`alias ls='ls --color=auto'`  
`alias network='sudo nmtui'`  
`alias fping='ping -c 100 -i .2'`  
`alias reboot='sudo /sbin/reboot'`  
`alias temp='vcgencmd measure_temp'`  
`alias t='traceroute'`  
`alias wifi=wavemon`  
`EOF`  
`source ~/.bashrc`

## *Bashrc para Alias*

`nano ~/.bashrc`  
`if [ -e $HOME/.bash_aliases ]; then`  
    `source $HOME/.bash_aliases`  
`fi`

# FSC Installs

```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg > /dev/null
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
wget -q "http://deb.playonlinux.com/public.gpg" -O- | sudo apt-key add -
sudo wget http://deb.playonlinux.com/playonlinux_bionic.list -O /etc/apt/sources.list.d/playonlinux.list
sudo apt update && sudo apt install deluge deluged emacs sublime-text tilix tigervnc-standalone-server xfonts-scalable xfonts-100dpi xfonts-75dpi --no-install-recommends wine wine32  winetricks mono-complete playonlinux nautilus-admin tilix vlc gparted wireguard exfatprogs hfsutils hfsprogs hfsutils dosfstools gparted

sudo apt install nautilus-image-converter nautilus-share gnome-sushi nautilus-admin

sudo apt install thunar-archive-plugin thunar-media-tags-plugin thunar-volman

#github
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
	&& sudo mkdir -p -m 755 /etc/apt/keyrings \
    	&& out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
    	&& cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
	&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
	&& sudo apt update \
	&& sudo apt install gh -y
```

# Arduino

`sudo usermod -a -G dialout f    #enable usb for user f`

1. `open up Arduino`  
2. `choose "Settings" from the "File" menu`  
3. `paste "http://arduino.esp8266.com/stable/package_esp8266com_index.json" into "Additional Board Manager URLs"`  
4. `open up the "Board Manager" from "Tools" menu, install "esp8266"`  
5. `connect your device via usb`  
6. `look for a newly found port (probably /dev/ttyUSB0)`  
7. `choose the right device from the list of boards (NodeMCU 1.0)`  
8. `there you go...`

# Backup

## *rsync*

#### ***`sudo tee /mnt/monet/backup/backup.sh > /dev/null << 'EOF'`***

#### ***`#!/bin/bash`***

#### 

#### ***`# Define the backup directory`***

#### ***`BACKUP_DIR="/mnt/monet/backup"`***

#### 

#### ***`# Rotate the backups (move pi5-3 to pi5-4, pi5-2 to pi5-3, etc.)`***

#### ***`if [ -d "$BACKUP_DIR/pi5-4" ]; then`***

####     ***`rm -rf "$BACKUP_DIR/pi5-4"`***

#### ***`fi`***

#### ***`if [ -d "$BACKUP_DIR/pi5-3" ]; then`***

####     ***`mv "$BACKUP_DIR/pi5-3" "$BACKUP_DIR/pi5-4"`***

#### ***`fi`***

#### ***`if [ -d "$BACKUP_DIR/pi5-2" ]; then`***

####     ***`mv "$BACKUP_DIR/pi5-2" "$BACKUP_DIR/pi5-3"`***

#### ***`fi`***

#### ***`if [ -d "$BACKUP_DIR/pi5-1" ]; then`***

####     ***`mv "$BACKUP_DIR/pi5-1" "$BACKUP_DIR/pi5-2"`***

#### ***`fi`***

#### 

#### ***`# Move the current backup (pi5) to pi5-1 to preserve the previous backup`***

#### ***`if [ -d "$BACKUP_DIR/pi5" ]; then`***

####     ***`mv "$BACKUP_DIR/pi5" "$BACKUP_DIR/pi5-1"`***

#### ***`fi`***

#### 

#### ***`# Perform the new backup, hard-linking unchanged files to pi5-1 to save space`***

#### ***`sudo rsync -aAXv --delete --link-dest="$BACKUP_DIR/pi5-1" --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/media/*","/lost+found","/mnt/*/*"} --include="/mnt/*/" / "$BACKUP_DIR/pi5"`***

#### 

#### ***`# Print completion message`***

#### ***`echo "Backup completed. Stored in $BACKUP_DIR/pi5"`***

#### ***`EOF`***

#### 

#### 

#### 

#### 

`chmod +x backup.sh`  
`crontab -e    # daily at midnight`  
`0 0 * * * /mnt/monet/backup/backup.sh`

`sudo rsync -aAXv /mnt/external/backup/root/ / 	#restore`

# Bluetooth Speaker

`ai pulseaudio pulseaudio-module-bluetooth`  
`sudo usermod -a -G bluetooth f`  
`sudo nano /etc/bluetooth/main.conf`  
`Class = 0x41C`  
`DiscoverableTimeout = 0`  
`sudo systemctl restart bluetooth`  
`bluetoothctl`  
`power on`  
`discoverable on`  
`pairable on`  
`agent on`  
`default-agent`  
`quit`  
`pulseaudio --start`  
`sudo systemctl status bluetooth`

# Deluge

## *Raspberry Pi*

`sudo apt-get update`  
`sudo apt-get install deluged deluge-web deluge-console -y`

`# user: debian-deluged`  
`sudo addgroup share`  
`sudo usermod -aG share debian-deluged`  
`sudo usermod -aG debian-deluged plex`  
`sudo usermod -aG share f`  
`sudo usermod -aG debian-deluged f	#rw deluged user`

`sudo nano /lib/systemd/system/deluged.service`  
	`UMask=0002`  
`User=debian-deluged`  
`Group=share`

`sudo systemctl daemon-reload`  
`sudo systemctl enable deluged`  
`sudo systemctl start deluged`

`systemctl status deluged`

`sudo nano /var/lib/deluged/config/auth			# user accounts`

#### ***`f:a:10`***

`------`  
`sudo nano /var/lib/deluged/config/core.conf  # configuration file`  
`sudo nano /var/lib/deluged/config/web.conf		# web configuration file`

## *Uninstall Completely*

`sudo systemctl stop deluged`  
`sudo systemctl stop deluge-web`  
`sudo apt-get purge deluge deluged deluge-web deluge-common deluge-console`  
`sudo apt-get autoremove && sudo apt-get autoclean`  
`rm -rf ~/.config/deluge`  
`sudo rm -rf /var/lib/deluge`  
`sudo rm -rf /var/lib/deluged`

## *linux*

`sudo nano /etc/systemd/system/deluged.service`

#### ***`[Unit]`***

#### ***`Description=Deluge Bittorrent Client Daemon`***

#### ***`Documentation=man:deluged`***

#### ***`After=network-online.target`***

#### 

#### ***`[Service]`***

#### ***`Type=simple`***

#### ***`ExecStart=/usr/bin/deluged -d`***

#### ***`Restart=on-failure`***

#### ***`User=deluge`***

#### ***`Group=share`***

#### ***`UMask=002`***

#### 

#### ***`[Install]`***

#### ***`WantedBy=multi-user.target`***

#### 

`sudo systemctl enable deluged`  
`sudo systemctl start deluged`

`sudo systemctl daemon-reload`   
`sudo systemctl restart deluged`  
`sudo systemctl status deluged`

`sudo nano /etc/systemd/system/deluge-web.service`

#### ***`[Unit]`***

#### ***`Description=Deluge Web Interface`***

#### ***`After=network-online.target deluged.service`***

#### ***`Wants=deluged.service`***

#### 

#### ***`[Service]`***

#### ***`Type=simple`***

#### ***`User=deluge`***

#### ***`Group=share`***

#### ***`UMask=002`***

#### ***`ExecStart=/usr/bin/deluge-web`***

#### ***`Restart=on-failure`***

#### 

#### ***`[Install]`***

#### ***`WantedBy=multi-user.target`***

### 

`sudo systemctl enable deluge-web`  
`sudo systemctl start deluge-web`

`hostname -I`

`sudo systemctl status deluge-web`

`deluge-console "config -s allow_remote True"`

### 

`sudo killall deluged`

`sudo nano /home/deluge/.config/deluge/auth`

#### ***`localclient……`***

#### ***`f:a:10`***

#### 

`sudo systemctl start deluged`

# Desktop Icons Launcher

## *Arronax*

`sudo apt update && sudo apt install arronax arronax-*`  
`au`  
`sudo apt update && sudo apt install arronax arronax-*`

## *Mlauncher*

# Docker-deluge

`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FD9B7DA1F26533EA`  
`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C5E6A5ED249AD24C`  
`sudo apt update`  
`curl -fsSL https://get.docker.com -o get-docker.sh`  
`sudo sh get-docker.sh`  
`docker --version`  
`sudo usermod -aG docker $USER`

`sudo apt install docker-compose-plugin`  
`sudo docker pull linuxserver/deluge`

`sudo mkdir -p /opt/stacks/deluge`  
`cd /opt/stacks/deluge`

`id deluge`  
`getent group share`

`sudo nano /opt/stacks/deluge/docker-compose.yml`

#### ***`version: '3'`***

#### ***`services:`***

####   ***`deluge:`***

####     ***`image: lscr.io/linuxserver/deluge:latest`***

####     ***`container_name: deluge`***

####     ***`environment:`***

####       ***`- PUID=1003	# deluge id`***

####       ***`- PGID=1002	# share group id`***

####       ***`- TZ=Europe/London  # Change this to your timezone`***

####     ***`volumes:`***

####       ***`- ./config:/config`***

####       ***`- /mnt/monet/downloads:/downloads  # Change this to your desired download path`***

####     ***`ports:`***

####       ***`- 8112:8112  # Web UI`***

####       ***`- 6881:6881  # Torrent port`***

####       ***`- 6881:6881/udp`***

####       ***`- 58846:58846  # Daemon port (optional)`***

####     ***`restart: unless-stopped`***

#### 

`sudo docker-compose up -d`

`docker exec -it deluge /bin/bash`  
`vi /config/auth`

#### ***`username:password:10`***

`docker restart deluge`  
`sudo systemctl enable docker`

# Docker-Pihole

`#Pi-hole can efficiently handle this if it has good caching and an external upstream DNS (like Unbound or a DNS resolver on a stronger server).`   
`#Pi 5 can handle 15-20k DNS queries/s, with unbound 5-10k Q/s: 5k+ users`  
`#Pi4 can handle 5-10k QPS, w/ unbound 1-4k: 2k users`  
`#5k users 1-2k QPS`

## *install docker container*

`# install docker https://pimylifeup.com/raspberry-pi-docker/`   
`curl -sSL https://get.docker.com | sh`  
`sudo usermod -aG docker $USER`

`# pihole docker https://pimylifeup.com/pi-hole-docker/`   
`sudo mkdir -p /opt/stacks/pihole`  
`cd /opt/stacks/pihole`

`sudo nano compose.yaml`  
`services:`  
  `pihole:`  
	`container_name: pihole`  
	`image: pihole/pihole:latest`  
	`ports:`  
  	`- "53:53/tcp"`  
  	`- "53:53/udp"`  
  	`- "67:67/udp"`  
  	`- "8080:80/tcp"`  
	`environment:`  
  	`TZ: 'America/Bogota'`  
  	`WEBPASSWORD: 'Alma8080'`  
	`volumes:`  
  	`- './etc-pihole:/etc/pihole'`  
  	`- './etc-dnsmasq.d:/etc/dnsmasq.d'`  
	`cap_add:`  
  	`- NET_ADMIN`  
	`restart: unless-stopped`

`docker compose up -d`

`#admin interface`  
[`http://10.88.0.8:8080/admin`](http://10.88.0.8:8080/admin)

`docker exec -it pihole bash		# shell in container`  
`pihole -g	# Update blocklists`  
`pihole -b	# Blacklist domains`  
`nslookup 	# Test DNS resolution`  
`cat /etc/resolv.conf  # Check which DNS server Pi-hole is using`  
`pihole -c	# pihole status`

`#test`  
`nslookup doubleclick.net`  
`nslookup doubleclick.net 10.88.0.8`  
`nslookup google.com`  
 

`#update pihole docker`  
`cd /opt/stacks/pihole`  
`docker compose pull`  
`docker compose up -d`

### **Performance**

`#Cache in the pihole instance`  
`sudo nano /etc/dnsmasq.d/01-pihole.conf`  
`cache-size=10000`  
`pihole restartdns`

### **\#RATE-Limiting**

`#in the container insure no ratelimit`  
`nano /etc/pihole/pihole-FTL.conf	#avoid default rate_limit`  
	`RATE_LIMIT=0/0`  
`or	RATE_LIMIT=50000/60`

`pihole restartdns`  
`grep RATE_LIMIT /var/log/pihole-FTL.log #verify no RATE_LIMIT`

`for i in {1..2000}; do nslookup google.com 10.88.0.8; done  #check limiting`

### **reliable blocklists**

`Step 1: Choose Reliable Blocklists`

`Here are some public blocklists you can use (you can add more based on your needs):`

* **`General Ad & Tracker Blocking`**  
  * `https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts`  
* **`Pornography Blocklists`**  
  * `https://blocklist.site/app/dl/porn.txt`  
  * `https://raw.githubusercontent.com/anudeepND/blacklist/master/adservers.txt`  
* **`Gambling Blocklists`**  
  * `https://blocklist.site/app/dl/gambling.txt`  
* **`Malware & Phishing`**  
  * `https://raw.githubusercontent.com/hoshsadiq/adblock-nocoin-list/master/hosts`


  

## *install Unbound*

`sudo apt update`  
`sudo apt install unbound -y`

`sudo nano /etc/unbound/unbound.conf.d/pi-hole.conf`  
`server:`  
	`verbosity: 1`  
	`interface: 127.0.0.1`  
	`port: 5335`  
	`do-ip4: yes`  
	`do-ip6: no`  
	`do-udp: yes`  
	`do-tcp: yes`  
	`root-hints: "/var/lib/unbound/root.hints"`  
	`cache-min-ttl: 3600`  
	`cache-max-ttl: 86400`  
	`harden-glue: yes`  
	`harden-dnssec-stripped: yes`  
	`use-caps-for-id: no`  
	`edns-buffer-size: 1232`  
	`prefetch: yes`  
	`num-threads: 4`

`sudo wget -O /var/lib/unbound/root.hints https://www.internic.net/domain/named.cache`

`sudo systemctl restart unbound`  
`sudo systemctl enable unbound`

# DNS suffix

`sudo nano /etc/resolv.conf`

`#add search path as follows for sweet.home domain:`  
`search redsi.co`

# Crontab

[`https://www.tecmint.com/11-cron-scheduling-task-examples-in-linux/`](https://www.tecmint.com/11-cron-scheduling-task-examples-in-linux/)  
[`https://www.tecmint.com/create-and-manage-cron-jobs-on-linux/`](https://www.tecmint.com/create-and-manage-cron-jobs-on-linux/)  
[`https://wiki.crowncloud.net/?How_to_Install_Zeit_Tool_on_Linux`](https://wiki.crowncloud.net/?How_to_Install_Zeit_Tool_on_Linux)

# Dynamic DNS

[`https://webmasters.stackexchange.com/questions/76739/what-is-the-update-url-for-dynamic-dns-for-google-domains#:~:text=The%20real%20Update%20URL%20is,url.`](https://webmasters.stackexchange.com/questions/76739/what-is-the-update-url-for-dynamic-dns-for-google-domains#:~:text=The%20real%20Update%20URL%20is,url.)  
[`https://cloud-jake.medium.com/google-domains-dynamic-dns-with-google-domains-1dd0ea45c219`](https://cloud-jake.medium.com/google-domains-dynamic-dns-with-google-domains-1dd0ea45c219)  
`https://[usuario]:[clave]@domains.google.com/nic/update?hostname=[subdominio].redsi.co&myip=[ip.ip.ip.ip]`

`curl "https://j6IxIi737NP61Sdo:je8Lk3HiCgAO3EgQ@domains.google.com/nic/update?hostname=ctrl.redsi.co">>ip.txt`

`#can be put in a crontab and run every 15 min`  
`*/15 * * * * /home/ubuntu/ip.sh`

# Fan control

### **ai fancontrol**

### **sudo pwmconfig**

# File Systems

## *BTRFS*

### **Ubuntu on btrfs (24.10)**

[`https://mattmoore.io/posts/btrfs-ubuntu-arch/`](https://mattmoore.io/posts/btrfs-ubuntu-arch/)   
[`https://mattmoore.io/posts/btrfs-ubuntu-subvolume/`](https://mattmoore.io/posts/btrfs-ubuntu-subvolume/) 

`#After installation`

	`lsblk`  
	`look for`  
	`├─nvme0n1p1 259:1	0   514M  0 part /target/boot/efi`  
	`├─nvme0n1p4 259:4	0 273.7G  0 part /target`  
	`sudo btrfs subvolume snapshot /target /target/@ubuntu`  
	`sudo umount -R /target`  
	`sudo mount -o subvol=@ubuntu /dev/nvme0n1p4 /target`  
	`sudo mount /dev/nvme0n1p1 /target/boot/efi`  
	`sudo mount --bind /dev /target/dev`  
	`sudo mount --bind /sys /target/sys`  
	`sudo mount --bind /proc /target/proc`

	`sudo chroot /target`

`#Update /etc/fstab`  
	`nano /etc/fstab`  
	`/dev/disk/by-uuid/13eac72c-db6f-4341-b691-e98ea97c9453 / btrfs subvol=@ubuntu 0 1`

	`grub-install`  
	`update-grub`  
	`update-initramfs -u -k all`  
	`exit`  
	`sudo umount -R /target`  
      
	`reboot`

`#Verify subvolume is active`  
	`ls /  #should not see @ubuntu`

`#Clean up root Ubuntu install now that subvolume is working`  
`sudo mount /dev/nvme0n1p4 /mnt`  
`cd /mnt`  
`ls`  
`sudo rm -rf bin boot dev home lib64 media opt root sbin snap sys var bin.usr-is-merged cdrom etc lib lib.usr-is-merged mnt proc run sbin.usr-is-merged srv tmp usr`  
`cd ~`  
`sudo umount -R /mnt`

### **MINT btrfs**

`mount btrfs`  
	`sudo btrfs subvolume snapshot /mnt/btrfs/@ /mnt/btrfs/@mint`  
	`sudo btrfs subvolume snapshot /mnt/btrfs/@home /mnt/btrfs/@mint-home`

	`sudo mount -o subvol=@mint /dev/nvme0n1p4 /mnt/btrfs`  
	`sudo mount /dev/nvme0n1p1 /mnt/btrfs/boot/efi`  
	`sudo mount --bind /dev /mnt/btrfs/dev`  
	`sudo mount --bind /sys /mnt/btrfs/sys`  
	`sudo mount --bind /proc /mnt/btrfs/proc`

	`sudo chroot /mnt/btrfs`  
	`nano /etc/fstab`  
	`/dev/disk/by-uuid/13eac72c-db6f-4341-b691-e98ea97c9453 / btrfs subvol=@mint 0 1`  
	`/dev/disk/by-uuid/13eac72c-db6f-4341-b691-e98ea97c9453 /home btrfs subvol=@mint-home 0 2`

	`grub-install`  
	`update-grub`  
	`update-initramfs -u -k all`  
`reboot`  
`sudo mount /dev/nvme0n1p4 /mnt`  
`sudo btrfs subvolume delete ./@`  
`sudo btrfs subvolume delete ./@home`  
`cd ..`  
`sudo umount /dev/nvme0n1p4`

`sudo nano /etc/grub.d/40_custom`  
`menuentry "Ubuntu" {`  
	`insmod btrfs`  
	`search --no-floppy --fs-uuid --set=root 13eac72c-db6f-4341-b691-e98ea97c9453`  
	`set subvol=@ubuntu`  
	`linux /$subvol/boot/vmlinuz root=UUID=13eac72c-db6f-4341-b691-e98ea97c9453 rootflags=subvol=@ubuntu ro quiet splash`  
	`initrd /$subvol/boot/initrd.img`  
`}`  
`#make sure the files exist or make symlink`  
	`sudo ln -s $subvol/boot/initrd.img-6.11.0-9-generic $subvol/boot/initrd.img`

`sudo update-grub`

### **Btrfs Snapshots**

`sudo mkdir -p /.snapshots`  
`sudo btrfs subvolume snapshot / /.snapshots/pop_snapshot_$(date +%Y%m%d) #-r for read only`  
`sudo btrfs subvolume list /`  
`# Delete a specific snapshot:`  
`sudo btrfs subvolume delete /media/f/btrfs/@ubuntu/.snapshots/ubuntu_snapshot_20241229`

### **Multiboot BTRFS**

### **Pop OS\! BTRFS and timeshift**

[`https://github.com/spxak1/weywot/blob/main/Pop_Btrfs_Subvolumes_with_Timeshift.md`](https://github.com/spxak1/weywot/blob/main/Pop_Btrfs_Subvolumes_with_Timeshift.md)

## *Pop OS Commands*

 `sudo update-alternatives --config x-terminal-emulator`

## *Pop OS\! Fix Boot*

[`https://support.system76.com/articles/bootloader/`](https://support.system76.com/articles/bootloader/)

```
[ -d /sys/firmware/efi ] && echo "Installed in UEFI mode" || echo "Installed in Legacy mode"
```

`# boot in live`  
`sudo mount /dev/nvme0n1p3 /mnt #mount the subvolume`  
`sudo mount /dev/nvme0n1p1 /mnt/boot/efi`

```
for i in dev dev/pts proc sys run; do sudo mount -R /$i /mnt/$i; done
sudo chroot /mnt
apt install --reinstall linux-image-generic linux-headers-generic
update-initramfs -c -k all
exit
sudo bootctl --path=/mnt/boot/efi install
```

## 

## *fstab*

**`# <file system>	<mount point>	<type>	<options> 		 <dump> <pass>`**  
**`# -----------------------------------------------------------------------`**

### **performance**

`,lazytime,noatime,x-systemd.automount,x-systemd.mount-timeout=30,x-systemd.idle-timeout=5min`

### **speed**

`/dev/sdb1                               /mnt/big      	ext4	noatime,nodiratime,users,rw,nofail,x-gvfs-show,x-systemd.automount,x-systemd.mount-timeout=60,x-systemd.idle-timeout=5min,async	0 2`  
`UUID=71713139456CFEE0                   		/mnt/installers	ntfs	noatime,nodiratime,users,rw,nofail,x-systemd.automount,x-systemd.mount-timeout=60,x-systemd.idle-timeout=5min,async	0 0`

### **ext4**

   	 `sudo mkfs.ext4 /dev/sda1 -L untitled	    #Format a drive to EXT4`

### **btrfs**

`UUID=767B-7724	/          	btrfs		subvol=/@,defaults,noatime,autodefrag,discard,ssd,space_cache,commit=120,compress=zstd`  
 				`0 0`

#### ***`commands`***

`sudo btrfs subvolume create /mnt/btrfs/@pop`  
`sudo btrfs subvolume list /mnt/btrfs`

`sudo btrfs check /dev/nvme0n1p4	#check`  
`sudo btrfs scrub start /mnt/btrfs	#scrub`  
`sudo btrfs scrub status /mnt/btrfs	#check the scrub`

### **exfat**

`ai exfatprogs`  
`UUID=767B-7724	/mnt/monet 	exfat 	defaults,user,uid=f,gid=share,fmask=0002,dmask=0002,umask=0002,nodev,nofail	0 0`

### **NTFS**

`UUID=767B-7724	/mnt/SD		ntfs		defaults,uid=f,gid=f,nofail,dmask=0022,fmask=0022,windows_names         	0 2`

`sudo mkfs.ntfs /dev/sda1 -f -v -I -L untitled	    #Format a drive to NTFS`

### **HFS+**

`sudo apt-get install hfsutils hfsprogs hfsutils	    #Add Apple OS X HFS+ read/write support`

`UUID=767B-7724  	/mnt/hfs+		hfplus	defaults   0   0`

`sudo mkfs.hfsplus /dev/sda1 -v untitled	#Format a drive to HFS+`

### **fat32**

`sudo apt-get install dosfstools	    #Add FAT32 read/write support`  
`sudo mkfs.vfat /dev/sda1 -n untitled	    #Format a drive to FAT32`

### **Timecapsule**

`sudo apt install samba`  
`sudo emacs /etc/samba/smb.conf`  
`[TimeMachine]`  
`path = /mnt/monet/backup/timecapsule`  
`valid users = @backup`  
`read only = no`  
`vfs objects = fruit streams_xattr	# mac and win extended attributes`  
`fruit:aapl = yes`  
`fruit:time machine = yes`  
`fruit:time machine max size = 1T`  
`create mask = 0660`  
`directory mask = 2770    #insures new files have the same group as their parent directories`  
`sudo systemctl restart smbd nmbd`

`sudo chmod g+s /mnt/monet/backup/timecapsule #makes all files in the same group of the directory`

## *USB Drives*

### **Automount options**

`id`  
`getent group share`  
`sudo nano /etc/udisks2/99-usb-mount-options.conf`

#### ***`[defaults]`***

#### ***`mount-options=uid=1000,gid=1001,fmask=0027,dmask=0027`***

#### 

#### 

`sudo systemctl restart udisks2`  
`udisksctl power-off -b /dev/sdc1 # to power down the usb`  
`udisksctl mount -b /dev/sdc1 	# to remount`

### **\#list drives**

`lsblk 	#list drives`

`sudo fdisk -l`  
`sudo mount -l`  
`df -h  #get free diskspace`

## *Ownership of files*

`sudo chown -R plex:plex .`

`nano ~/plexown.sh`

#### ***`sudo find /mnt/media -type d \! -perm 775 -exec chmod 775 {} \; -print`***

#### ***`sudo find /mnt/media -type f \! -perm 664 -exec chmod 644 {} \; -print`***

#### ***`sudo find /mnt/media         \! -user plex -exec chown plex.plex {} \; -print`***

`sudo chmod +x ~/plexown.sh`

## *Size of subfolders*

 `du -sh ./* | sort -h`

## *List partitions*

`lsblk -f	#as a tree with uuid`  
`blkid`

# Firewall

#### 

`sudo ufw allow 32400/tcp comment 'Allow Plex Media Server'`  
`sudo ufw allow 6881:6891/tcp comment 'Allow BitTorrent traffic'`  
`sudo ufw allow 6881:6891/udp comment 'Allow BitTorrent traffic'`  
`sudo ufw allow 22/tcp comment 'Allow SSH'`  
`sudo ufw allow 80/tcp comment 'Allow HTTP traffic'`  
`sudo ufw allow 443/tcp comment 'Allow HTTPS traffic'`  
`sudo ufw allow 5900/tcp comment 'Allow VNC for remote desktop access'`  
`sudo ufw allow 3389/tcp comment 'Allow RDP for remote desktop access'`  
`sudo ufw allow 58846/tcp comment 'Allow Deluge RPC'`

`# Allow traffic from 192.168.2.0/24`  
`sudo ufw allow from 192.168.2.0/24 comment 'Allow traffic from 192.168.2.0/24'`

`# Allow traffic from 10.0.0.0/8`  
`sudo ufw allow from 10.0.0.0/8 comment 'Allow traffic from 10.0.0.0/8'`

`# Allow traffic from 192.168.12.0/24`  
`sudo ufw allow from 192.168.12.0/24 comment 'Allow traffic from 192.168.12.0/24'`

`sudo ufw allow 21/tcp comment 'Allow FTP'`  
`sudo ufw allow 137,138/udp comment 'Allow NetBIOS for SMB/CIFS file sharing'`  
`sudo ufw allow 139,445/tcp comment 'Allow SMB/CIFS file sharing'`

## *Plex*

[`https://gist.github.com/nmaggioni/45dcca7695d37e6109276b1a6ad8c9c9`](https://gist.github.com/nmaggioni/45dcca7695d37e6109276b1a6ad8c9c9)  
`sudo nano /etc/ufw/applications.d/plexmediaserver`

#### ***`[plexmediaserver]`***

#### ***`title=Plex Media Server (Standard)`***

#### ***`description=The Plex Media Server`***

#### ***`ports=32400/tcp|3005/tcp|5353/udp|8324/tcp|32410:32414/udp`***

#### 

#### ***`[plexmediaserver-dlna]`***

#### ***`title=Plex Media Server (DLNA)`***

#### ***`description=The Plex Media Server (additional DLNA capability only)`***

#### ***`ports=1900/udp|32469/tcp`***

#### 

#### ***`[plexmediaserver-all]`***

#### ***`title=Plex Media Server (Standard + DLNA)`***

#### ***`description=The Plex Media Server (with additional DLNA capability)`***

#### ***`ports=32400/tcp|3005/tcp|5353/udp|8324/tcp|32410:32414/udp|1900/udp|32469/tcp`***

#### 

#### ***`sudo ufw app update plexmediaserver`***

#### ***`sudo ufw allow plexmediaserver-all`***

`The following additional ports are also used within the local network for different services (local network):`

* `UDP: 1900 (access to the Plex DLNA Server)`

* `UDP: 5353 (older Bonjour/Avahi network discovery)`

* `TCP: 8324 (controlling Plex for Roku via Plex Companion)`

* `UDP: 32410:32414 (current GDM network discovery)`

* `TCP: 32469 (access to the Plex DLNA Server)`


  

### 

# GRUB

### **`Customize GRUB in /etc/default/grub:`**

1. **`Remove advanced entries:`**  
   **`GRUB_DISABLE_SUBMENU=y`**

2. **`Set 1080p resolution and keep during boot:`**  
   **`GRUB_GFXMODE=1920x1080`**   
   **`GRUB_GFXPAYLOAD_LINUX=keep`**  
3. **`Increase font size for readability:`**  
   **`GRUB_FONT=/boot/grub/fonts/large.pf2`**   
   **`# To create a larger font:`**   
   **`sudo grub-mkfont --output=/boot/grub/fonts/large.pf2 --size=32 /usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf`**   
4. **`Apply changes:`**  
   **`sudo update-grub`**  
     
     
   `sudo update-grub   # updates grub to /boot/grub/grub.conf`  
     
   `#Change Resolution`  
   `xdpyinfo | awk '/dimensions/{print $2}' 	#find resolution`  
   `sudo nano /etc/default/grub`   
   `edit the line GRUB_GFXMODE=[width]x[height]x32`  
   `sudo grub-mkconfig -o /boot/grub/grub.cfg	#update grub config`  
     
   `#change colors`  
   `sudo editor /etc/grub.d/06_local_colors`  
   `#!/bin/sh`  
   `# /etc/grub.d/06_local_colors`  
   `# Override foreground/background colors with local admin's choices.`    
   `#`  
   `# Note: be sure to chmod +x this file or it will not be used.`  
   `# After editing this file, run update-grub.`  
   `set -e`  
   `echo "Overriding foreground/background text colors ($0)" >&2`  
     
   `echo "${1}set color_normal=light-gray/black"`  
   `echo "${1}set color_highlight=black/light-gray"`  
     
   `# Set these if you'd like the menu options to be different than other text`  
   `echo "${1}set menu_color_normal=light-gray/black"`  
   `echo "${1}set menu_color_highlight=black/light-gray"`  
     
   `# NOTES`  
   `# Colors: red, green, blue, cyan, magenta, brown, light-gray, black`  
   `#`  
   `# Foreground has additional colors available:`  
   `#`  
   `#     	light-red, light-green, light-blue`  
   `#     	light-cyan, light-magenta, yellow, white, dark-gray`  
   `# Text background of "black" is transparent when a background image exists.`  
   `# (GRUB_BACKGROUND in /etc/default/grub).`  
   `# To change the font face and size, set GRUB_FONT in /etc/default/grub`  
   `# to point to a .pf2 file crated by grub-mkfont.`  
   `#`  
   `# sudo grub-mkfont --output=/boot/grub/fonts/DejaVuSansMono24.pf2 --size=24 \`  
   `#       	/usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf`  
     
   `sudo chmod +x /etc/grub.d/06_local_colors`  
   `sudo update-grub`  
     
   `#change font`  
   `sudo grub-mkfont --output=/boot/grub/fonts/DejaVuSansMono24.pf2 --size=24 /usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf`  
     
   `set GRUB_FONT in /etc/default/grub`  
     
   `sudo add-apt-repository ppa:danielrichter2007/grub-customizer`  
   `sudo apt-get update`  
   `sudo apt-get install grub-customizer`

# Google-Drive-Ocamfuse

### **sudo add-apt-repository ppa:alessandro-strada/ppa**

### **sudo apt update && sudo apt install google-drive-ocamlfuse**

### **google-drive-ocamlfuse**

### **mkdir \~/googledrive**

### **google-drive-ocamlfuse \~/googledrive**

### 

### **fusermount \-u \~/google-drive  \#to unmount**

# GNS3

## *Promiscous Mode*

`Ref: https://bbs.archlinux.org/viewtopic.php?id=65508`

`1/ Method 1`  
`# First, create a new Linux group which has permission to use promiscuous mode, and add yourself to the group.`  
`$ groupadd promiscuous`  
`$ usermod -a -G promiscuous <your_user_id>`  
`# Update the group ownership and access permission of /dev/vmnet*`  
`$ chgrp promiscuous /dev/vmnet*`  
`$ chmod g+rw /dev/vmnet*`

`2/ Method 2`  
`To allow all users (instead of a specific user) to set the virtual adapter to promiscuous mode, run the following command on host machine.`  
`$ sudo chmod a+rw /dev/vmnet*`

### **To make it permanent at each reboot==**

`# For Method 1 (assuming that you already created a Linux group called "promiscuous" as described earlier):`  
`Find vmwareStartVmnet in sudo nano /etc/init.d/vmware`  
`vmwareStartVmnet() {`  
  `vmwareLoadModule $vnet`  
  `"$BINDIR"/vmware-networks --start >> $VNETLIB_LOG 2>&1`  
  `chgrp promiscuous /dev/vmnet*`  
  `chmod g+rw /dev/vmnet*`  
`}`  
`# For Method 2 :`  
`Find the line vmwareStartVmnet in /etc/init.d/vmware, and put the chmod as below :`  
`vmwareStartVmnet()`  
  `vmwareLoadModule $vnet`  
  `"$BINDIR"/vmware-networks --start >> $VNETLIB_LOG 2>&1`  
  `chmod a+rw /dev/vmnet*`  
`}`

# Harddrive Speed

## *fio*

```py
# Define color variables
YELLOW='\033[1;33m'
NC='\033[0m' # No Color

echo -e "${YELLOW}Large File Write Speed${NC}"
echo -e "${YELLOW}=================${NC}"
fio --name=copy_movies --rw=write --size=2G --blocksize=1M --direct=1 --numjobs=1 --group_reporting --filename=movies.img | grep -E 'WRITE: bw='

echo -e "${YELLOW}Large File Read Speed${NC}"
echo -e "${YELLOW}=================${NC}"
fio --name=read_movies --rw=read --size=2G --blocksize=1M --direct=1 --numjobs=1 --group_reporting --filename=movies.img | grep -E 'READ: bw='

echo -e "${YELLOW}Backup Speed (Mixed Read/Write)${NC}"
echo -e "${YELLOW}=================${NC}"
fio --name=backup --rw=randrw --rwmixread=70 --size=2G --blocksize=128K --direct=1 --numjobs=2 --iodepth=16 --group_reporting --filename=backup.img | grep -E 'READ: bw=|WRITE: bw='

echo -e "${YELLOW}Many Small Files Speed${NC}"
echo -e "${YELLOW}=================${NC}"
fio --name=copy_installers --rw=randwrite --size=256M --blocksize=4K --direct=1 --numjobs=2 --iodepth=16 --runtime=15 --time_based --group_reporting --filename=installers.img | grep -E 'WRITE: bw='




sudo dmesg | grep -i usb

sudo dmesg | grep -i usb









```

## *dd*

```py
#Write
sudo dd if=/dev/zero of=./tempfile bs=1M count=1024 conv=fdatasync
#Read
sudo sh -c "/usr/bin/echo 3 > /proc/sys/vm/drop_caches"
sudo dd if=./tempfile of=/dev/null bs=1M count=1024

```

[`https://github.com/geerlingguy/raspberry-pi-dramble/issues/7`](https://github.com/geerlingguy/raspberry-pi-dramble/issues/7)  
 `wget http://www.iozone.org/src/current/iozone3_430.tar`  
 `cat iozone3_430.tar | tar -x`  
 `cd iozone3_430/src/current`  
 `make linux-arm`  
`./iozone -e -I -a -s 100M -r 4k -r 512k -r 16M -i 0 -i 1 -i 2`

[`https://domoticproject.com/extending-life-raspberry-pi-sd-card/`](https://domoticproject.com/extending-life-raspberry-pi-sd-card/)

# Mount Network drive

`sudo mount -t cifs -o username=f,uid=1000 //10.85.0.8/monet /mnt/monet`

`fstab`  
`//10.85.0.8/monet /mnt/monet cifs username=f,password=Alma8080,uid=1000,gid=1002,file_mode=0644,dir_mode=0755,x-systemd.automount,nofail 0 0`

# NordVPN

[`https://support.nordvpn.com/hc/en-us/articles/20196094470929-Installing-NordVPN-on-Linux-distributions#h_01HGZ1TXZP1ENNRCY7EDCXV8XE`](https://support.nordvpn.com/hc/en-us/articles/20196094470929-Installing-NordVPN-on-Linux-distributions#h_01HGZ1TXZP1ENNRCY7EDCXV8XE)

`nordvpn connect United_States`  
`sudo wg show nordlynx private-key`  
`sudo wg show nordlynx`

`private_key=`   
`0Hx1kZa0WI78SZlDKITLdM+VsSub2tziFxVAzCN/oXE=`

# Plex

## *Pi*

[`https://pimylifeup.com/raspberry-pi-plex-server/`](https://pimylifeup.com/raspberry-pi-plex-server/)

`sudo apt-get update`  
`sudo apt-get upgrade`  
`sudo apt-get install apt-transport-https`  
`curl https://downloads.plex.tv/plex-keys/PlexSign.key | gpg --dearmor | sudo tee /usr/share/keyrings/plex-archive-keyring.gpg >/dev/null`  
`echo deb [signed-by=/usr/share/keyrings/plex-archive-keyring.gpg] https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list`  
`sudo apt-get update`  
`sudo apt install plexmediaserver`  
`hostname -I`  
`sudo nano /boot/cmdline.txt 	# older version`  
`sudo nano /boot/firmware/cmdline.txt`

#### ***`ip=YOUR IP  	# at the bottom of the file to set static ip`***

`sudo usermod -aG plex f`  
`sudo usermod -aG share plex`  
`sudo reboot`

`sudo chmod 2775 /mnt/monet/media #so files inherit directory group (chmod 2xxx )`

`emacs plexown.sh`  
`#!/bin/bash`

`# Process directories and their subdirectories`  
`sudo find /mnt/monet/media -type d \! -perm 2775 -exec chmod 2775 {} \; -print`

`# Process files only in subdirectories, excluding files directly under /mnt/monet/media`  
`sudo find /mnt/monet/media -mindepth 2 -type f \! -perm 664 -exec chmod 664 {} \; -print`

# Power

## *Lenovo*

`sudo add-apt-repository ppa:linrunner/tlp`  
`sudo apt update`  
`sudo apt install tlp tlp-rdw`  
`sudo nano /etc/tlp.conf`

#### ***`# ThinkPad specific charge thresholds`***

#### ***`# Charging starts when the remaining capacity falls below this percentage`***

#### ***`# Default: 0(off)`***

#### ***`# START_CHARGE_THRESH_BAT0=75`***

#### ***`# Charging stops when the remaining capacity exceeds this percentage`***

#### ***`# Default: 100(off)`***

#### ***`# STOP_CHARGE_THRESH_BAT0=80`***

`sudo systemctl enable tlp.service`  
`sudo systemctl start tlp.service`

`sudo tlp-stat  # check if running`

`sudo tlp-stat -b # current status`

### **samgung**

`echo '1' | sudo tee /sys/devices/platform/samsung/battery_life_extender`

# Sketchup

`WINEPREFIX=~/.wine64 winetricks --force dotnet452 corefonts`  
`WINEPREFIX=~/.wine32 winetricks dotnet40`

# Snap Install

### **sudo apt update**

### **sudo apt install snapd** 

### **sudo snap install snap-store**

# Secure FTP Server

## [*https://ubunlog.com/en/vsftpd-instalar-un-servidor-ftp-ubuntu/*](https://ubunlog.com/en/vsftpd-instalar-un-servidor-ftp-ubuntu/)

[`https://saturncloud.io/blog/how-to-install-and-configure-ftp-on-amazon-ec2/`](https://saturncloud.io/blog/how-to-install-and-configure-ftp-on-amazon-ec2/)  
`sudo apt install -y vsftpd`  
`sudo cp /etc/vsftpd.conf /etc/vsftpd.conf_default`  
`sudo systemctl start vsftpd`  
`sudo ufw allow 20/tcp; sudo ufw allow 21/tcp; sudo ufw allow 990/tcp; sudo ufw allow 40000:50000/tcp`  
`sudo nano /etc/vsftpd.conf`

### **sudo openssl req \-x509 \-nodes \-days 365 \-newkey rsa:2048 \-keyout /etc/ssl/private/vsftpd.pem \-out /etc/ssl/private/vsftpd.pem**

`sudo nano /etc/vsftpd.conf`

#### ***`rsa_cert_file=/etc/ssl/private/vsftpd.pem`***

#### ***`rsa_private_key_file=/etc/ssl/private/vsftpd.pem`***

#### ***`ssl_enable=YES`***

#### ***`allow_anon_ssl=NO`***

#### ***`force_local_data_ssl=YES`***

#### ***`force_local_logins_ssl=YES`***

#### ***`ssl_tlsv1=YES`***

#### ***`ssl_sslv2=NO`***

#### ***`ssl_sslv3=NO`***

#### ***`require_ssl_reuse=NO`***

#### ***`ssl_ciphers=HIGH`***

`sudo systemctl restart vsftpd`

## *Create SFTP user without shell*

[`https://www.digitalocean.com/community/tutorials/how-to-enable-sftp-without-shell-access-on-ubuntu-16-04`](https://www.digitalocean.com/community/tutorials/how-to-enable-sftp-without-shell-access-on-ubuntu-16-04)   
`sudo adduser sammyfiles`

```
sudo adduser redsiback
sudo mkdir -p /monet/backups/redsi
sudo chown redsiback:backup /monet/backups/redsi
sudo chmod 755 /monet/backups
sudo nano /etc/ssh/sshd_config
...
Match User redsiback
ForceCommand internal-sftp
PasswordAuthentication yes
ChrootDirectory /var/sftp
PermitTunnel no
AllowAgentForwarding no
AllowTcpForwarding no
X11Forwarding no

sudo systemctl restart sshd
```

# Samba SMB Share

`sudo apt-get install samba`  
`sudo smbpasswd -a f`

`sudo nano /etc/samba/smb.conf`

#### ***`[global]`***

####    ***`workgroup = (your workgroup name)`***

####    ***`wins support=yes`***  	

#### 

#### ***`[monet]`***

####   ***`comment = Monet drive on Raspberry Pi`***  

####   ***`path = /mnt/monet`***

####   ***`valid users = f lom`***

####   ***`browsable = yes`***

####   ***`writable = yes`***

   `available = yes`

   `guest ok = yes`  
   `public = no`  
   `force group = share`  
   `create mask = 0664			#rw owner and g, rx others`  
   `directory mask = 2775		#rwx owner and g, rx others, special inherit group`  
   `force create mode = 0664		# forces to 664`  
   `force directory mode = 2775	# forces to 2775`  
   `vfs objects = catia fruit streams_xattr	#winsoes and mac`

`sudo service smbd restart`  
`ai gadmin-samba`

# SSH Server

[`https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server`](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)  
[`https://phoenixnap.com/kb/ssh-permission-denied-publickey`](https://phoenixnap.com/kb/ssh-permission-denied-publickey)  
`sudo apt install openssh-server`  
`sudo systemctl is-enabled ssh`

`#private key`  
`mkdir -p ~/.ssh`  
`sudo chmod 700 ~/.ssh`  
`ssh-keygen -t rsa`

`#edit vsfpd config`  
`sudo nano /etc/ssh/sshd_config`

`PermitRootLogin no`  
`PubkeyAuthentication yes`  
`AuthorizedKeysFile      .ssh/authorized_keys .ssh/authorized_keys2`  
`PasswordAuthentication no`  
`KbdInteractiveAuthentication no`  
`ChallengeResponseAuthentication  #???`  
`UsePAM yes`

    `X11Forwarding yes`  
    `X11UseLocalhost no`

`#copy public keys to authorized_keys`  
`cat casa_id_rsa.pub >> ~/.ssh/authorized_keys`  
`systemctl restart sshd.service`

`ssh-copy-id username@host  #or this to copy automatically`

# Sublime Text

## *install*

`wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg > /dev/null`  
`echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list`  
`sudo apt-get update`  
`sudo apt-get install sublime-text`

## *winbox config*

`Open the command palette: Win/Linux: ctrl+shift+p,`  
`Type “Install Package Control”, press enter Restart Sublime Text`  
`Open the command palette: Win/Linux: ctrl+shift+p,`  
`Type “Install Package” <enter> “MikrotikScript`

# ---

# `RASPBERRY PI`

# Temperature

    `sudo armbianmonitor -M`

# VLANs

[`http://www.microhowto.info/howto/configure_an_ethernet_interface_as_a_vlan_trunk_on_debian.html`](http://www.microhowto.info/howto/configure_an_ethernet_interface_as_a_vlan_trunk_on_debian.html)  
[`https://blog.sleeplessbeastie.eu/2019/12/20/how-to-create-vlan-interface-using-the-ip-utility/`](https://blog.sleeplessbeastie.eu/2019/12/20/how-to-create-vlan-interface-using-the-ip-utility/)

`apt-get install vlan`

`nano /etc/network/interfaces`  
`# vlan`  
`auto eth0.10`  
`iface eth0.10 inet static`  
`address 186.96.114.238`  
`netmask 255.255.255.248`  
   	 `gateway 186.96.114.233`  
     	 `dns-nameservers 1.1.1.1 1.0.0.1`

`ifup eth0.10`

# VMware 17.6.1 Workstation

[`https://askubuntu.com/questions/1494239/gnu-c-compiler-gcc-version-12-2-0-was-not-found-vmware`](https://askubuntu.com/questions/1494239/gnu-c-compiler-gcc-version-12-2-0-was-not-found-vmware) 

```
apt install gcc-12
sudo apt install build-essential

# use
/usr/bin/gcc-12
```

# VNC-TigerVNC

[`https://github.com/gitbls/RPiVNCHowTo`](https://github.com/gitbls/RPiVNCHowTo)  
`sudo apt update && sudo apt upgrade`  
`sudo apt-get install tigervnc-standalone-server xfonts-scalable xfonts-100dpi xfonts-75dpi --no-install-recommends`  
`sudo nano /etc/tigervnc/vncserver-config-mandatory`

#### ***`# $localhost should the TigerVNC server only listen on localhost for`***

#### ***`#        	incoming VNC connections`***

#### ***`#`***

#### ***`# $localhost = "yes";`***

#### ***`$localhost = "no";`***

`sudo tigervncpasswd`  
`tigervncserver`

`connect with :5901 port`

# VNC RealVNC (dietpi)

[`https://dietpi.com/forum/t/realvnc-whats-going-on-with-realvnc/5879/6`](https://dietpi.com/forum/t/realvnc-whats-going-on-with-realvnc/5879/6)  
`#set service password`  
`sudo vncpasswd -service`  

# VPN

## *NordVPN*

`nordvpn countries`  
`nordvpn set country United_States`  
`nordvpn connect United_States`

# Web Lightweight

## The lightweight web server Lighttpd 1.4.31 can use all of its features on the Rasp Pi. Lighttpd offers important functions, is supported by many content management systems, and needs only minimal system resources

# Wine

[`https://forums.linuxmint.com/viewtopic.php?t=293766`](https://forums.linuxmint.com/viewtopic.php?t=293766)

```c
wget -q "http://deb.playonlinux.com/public.gpg" -O- | sudo apt-key add -
sudo wget http://deb.playonlinux.com/playonlinux_bionic.list -O /etc/apt/sources.list.d/playonlinux.list
sudo apt-get update
sudo apt-get install playonlinux
```

`sudo wget http://deb.playonlinux.com/playonlinux_bionic.list -O /etc/apt/sources.list.d/playonlinux.list`

`#fonts for winbox`

## *Winetricks*

`cd "${HOME}/Downloads"`  
`wget  https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks`  
`chmod +x winetricks`  
`./winetricks`  
`#install MS Fonts`

[`https://www.bytebang.at/Blog/Getting+Mikrotik+winbox+fonts+right+when+emulated+in+wine#`](https://www.bytebang.at/Blog/Getting+Mikrotik+winbox+fonts+right+when+emulated+in+wine#)  
`sudo apt install ttf-mscorefonts-installer #for winbox`

# WSL

## *mount disks*

[`https://learn.microsoft.com/en-us/windows/wsl/wsl2-mount-disk`](https://learn.microsoft.com/en-us/windows/wsl/wsl2-mount-disk)	  
[`https://learn.microsoft.com/en-us/windows/wsl/connect-usb`](https://learn.microsoft.com/en-us/windows/wsl/connect-usb)   
`GET-CimInstance -query "SELECT * from Win32_DiskDrive"   #identify disk. Usually under the \\.\PHYSICALDRIVE* format.`  
`wsl --mount <DiskPath> --bare  #not mount partitions`  
`wsl --mount <DiskPath>   #mount reconised partitions`  
`wsl`  
	`lsblk		#list partitions`

`wsl --unmount <DiskPath>`

# \----------------------------------------------------------------------------------

# 

# Useful commands

## *update firmware*

`sudo fwupdmgr refresh && sudo fwupdmgr update`

## *Chmod files to rw not exec, directories to rwx (permissions)*

[`https://www.multacom.com/faq/password_protection/file_permissions.htm#:~:text=777%20%2D%20all%20can%20read%2Fwrite%2Fsearch.,web%20store%20folder%2C%20CGI%20scripts`](https://www.multacom.com/faq/password_protection/file_permissions.htm#:~:text=777%20%2D%20all%20can%20read%2Fwrite%2Fsearch.,web%20store%20folder%2C%20CGI%20scripts)

`chmod -R a-x [directory]`  
`chmod -R a+rwX [directory]`

`# removes execute bit from all files and directories followed by adding read and write privileges to everything, and execute privileges to only directories. (No regular files have the execute bit on anymore from the first step.)`

## *Find pattern in directory*

`grep -rnw '/path/to/somewhere/' -e 'pattern'`

## *Size Subfolders*

`du -sh ./* | sort -h			#size of subfolders`

## *Manuals*

`tldr`

## *Processes*

`btop`  
`htop`

## *Users*

`sudo usermod -aG [group] [user]	# add user to group`  
`newgrp [group]				# update group membership without logging out`  
`sudo deluser [user] [group] 		#remove user from group`  
`sudo deluser [user]		 		#remove user`  
`less /etc/passwd  				# list users`  
`less /etc/group				# list groups`  
`groups [user]					# list groups of a user`

`sudo adduser [user]`

## *Add DNS suffix Resolve Domain*

`sudo nano /etc/systemd/resolved.conf #file to include your search domain`  
`[Resolve]`  
`Domains=yourdomain.com`

`sudo systemctl restart systemd-resolved`

## *File System*

### **Check EXT File System**

`sudo fsck -f -y /dev/sda1  #-f forces check even if clean`    
`sudo e2fsck -p -f -y -C 0 /dev/[sdb?]  #ext`

### **disks**

`df -h`  
`blkid`  
`lsblk` 

### **BTRFS**

`sudo btrfs subvolume create /data/photos			#auto creates directory`  
`sudo btrfs subvolume list /data					#shows subvolumes`  
`sudo btrfs subvolume show /data/projects			#details of subvolume`  
`sudo mount /dev/sdb1 -o subvol=projects /tmp/projects	#mount subvolume w/ name`  
`sudo mount /dev/sdb1 -o subvolid=261 /tmp/projects	#mount subvolume w/ id`  
`sudo btrfs subvolume delete /data/test				#remove subvolume`  
`sudo btrfs check --repair  /dev/nvme0n1p5`

##### *`Convert ext → BTRFS`*

`e2fsck -fvy /dev/sdx`

## *EFI Clean*

`sudo mount /dev/nvme0n1p1 /mnt	#mount EFI`

`sudo efibootmgr -v`  
`sudo efibootmgr -b <boot-number> -B`

`e.g. sudo rm -r /mnt/EFI/Linux`

# Anydesk

[`https://www.fosslinux.com/97204/how-to-install-anydesk-on-ubuntu.htm`](https://www.fosslinux.com/97204/how-to-install-anydesk-on-ubuntu.htm)  
`au`  
`wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | sudo apt-key add -`  
`echo "deb http://deb.anydesk.com/ all main" | sudo tee /etc/apt/sources.list.d/anydesk-stable.list`  
`au`  
`ai anydesk`  
`sudo anydesk --admin-settings`  
`sudo nano /etc/gdm3/custom.conf`

# L2TP

`au`  
`sudo apt install network-manager-l2tp network-manager-l2tp-gnome`  
`sudo systemctl restart NetworkManager`

# Permissions

`sudo chmod -R 775 *  # owner and group (rwx), others (rx)`  
`sudo chmod -R 774 *  # owner and group (rwx), others (r)`  
`sudo chmod -R 777 *  # owner others and group (rwx)`   
`sudo chmod -R 755 *  # Owner (rwx), group and other (rx)`   
`sudo chmod -R g+rw .	# add group rw`

`sudo chmod g+s /mnt/monet/media #make folder members inherit group (sudo chmod 2xxx)`

# Rsync

## [https://www.hostinger.es/tutoriales/rsync-linux](https://www.hostinger.es/tutoriales/rsync-linux)

`rsync [-avrhzP] SRC [USER@]HOST:[DEST]`  
	`-a permissions and time`  
	`-z compress`  
	`-h human readable`  
	`-r recursive`  
	`-v muestra progreso`  
	`-P muestra progreso y parcial`  
	`--delete para mirror borrando lo que no estar en destino`  
	`--exclude para no incluir estos archivos`  
	`--max-size 10k para no copiar archivos más grandes`

# Scripts

### **\#this changes .txt extensions to .csv**

#### ***`for f in *.txt; do`***

####     ***`mv "$f" "${f%.txt}.csv"`***

#### ***`done`***

# Repair Boot

### **sudo apt install software-properties-common; sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb\_release \-sc) universe"; sudo add-apt-repository \-y ppa:yannubuntu/boot-repair; sudo apt-get update; sudo apt-get install \-y boot-repair && boot-repair**

# Wifi Signal

`ai wavemon`  
`wavemon`

# Disable touch screen

`xinput -disable 12`

# Firewall

`sudo ufw disable`  
`sudo ufw status`  
`sudo ufw enable`

# System cleaner

`BleachBit`

# Bookworm Pup64

`nano ~/Startup/fsc.sh`  
`xinput set-prop "ELAN0B00:00 04F3:3136 Touchpad" "Synaptics Scrolling Distance" -70 -70 #natural scrolling`  
`chmod +x ~/Startup/fsc.sh`

## *Firefox*

[`https://support.mozilla.org/en-US/kb/install-firefox-linux?utm_source=www.mozilla.org&utm_medium=referral&utm_campaign=firefox-download-thanks#w_install-from-your-distribution-package-manager`](https://support.mozilla.org/en-US/kb/install-firefox-linux?utm_source=www.mozilla.org&utm_medium=referral&utm_campaign=firefox-download-thanks#w_install-from-your-distribution-package-manager) 

**`sudo ln -s /opt/firefox/firefox /usr/local/bin/firefox`**  
**`wget https://raw.githubusercontent.com/mozilla/sumo-kb/main/install-firefox-linux/firefox.desktop -P /usr/share/applications`**

`menu/setup/default apps #change browser`

## *bash prompt*

`nano ~/.bashrc`  
	`PS1='\u@\h:\w\$ '`

	`PS1='\[\e[1;32m\]\u@\h\[\e[0m\]:\[\e[1;34m\]\w\[\e[0m\]\$ '`

# Raspberry Pi

## *I2C LCD ([https://www.youtube.com/watch?v=DHbLBTRpTWM](https://www.youtube.com/watch?v=DHbLBTRpTWM))*

`sudo apt-get update -y && sudo apt-get install python3-smbus git i2c-tools -y`

`sudo raspi-config  ** Enable Interface I2C`  
`sudo reboot`  
`i2cdetect -l`  
`i2cdetect -y 1`  
`sudo pip3 install rpi_lcd --break-system-packages`

`sudo find /usr/local/ -name rpi_lcd 2> /dev/null`  
`f@pi:~ $ cd /usr/local/lib/python3.11/dist-packages/rpi_lcd`  
`f@pi:/usr/local/lib/python3.11/dist-packages/rpi_lcd $ sudo nano __init__.py # address 3f??`

## *Temperature DB32* 

`(https://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/temperature/#exampleCode)`

`#temp.py`  
`tfile = open("/sys/bus/w1/devices/28-0516a79f7aff/w1_slave")`  
`text1=tfile.read()`  
`tfile.close()`

`tfile = open("/sys/bus/w1/devices/28-0516a7a565ff/w1_slave")`  
`text2=tfile.read()`  
`tfile.close()`

`tfile = open("/sys/bus/w1/devices/28-0516a7a5bfff/w1_slave")`  
`text3=tfile.read()`  
`tfile.close()`

`temperature1 = float(text1.split("\n")[1].split(" ")[9][2:])/1000`  
`temperature2 = float(text2.split("\n")[1].split(" ")[9][2:])/1000`  
`temperature3 = float(text3.split("\n")[1].split(" ")[9][2:])/1000`

`print (temperature1)`  
`print (temperature2)`  
`print (temperature3)`

## *Wine Box64*

`#Install Pi Apps`  
`wget -qO- https://raw.githubusercontent.com/Botspot/pi-apps/master/install | bash`

## *install to emmc*

`Steps:`   
`To flash Android on the emmc (reference viewtopic.php?f=53&t=6173)`  
`Download this alpha file ->`  
`http://dn.odroid.com/5422/ODROID-XU3/An ... 06.img.zip`  
`Unzip with 7-Zip (Windows) or Linux using "xz -dk"`   
`Flash to a microSD card using Wind32disk imager for odroid http://bit.ly/1LVPcbF`   
`Setup ODROID-X board to boot of SD (Jumper).`  
`Make sure that the eMMC installer SDCARD and eMMC are connected.`   
`Turn on the board. Wait at least 15mins for the fully flash.`  
`After waiting 15 minutes, power off the board, remove the sdcard set the jumper to eMMC boot!`  
`Check if booted onto Android.`  
`You can check part of this steps on the ameridroid video (https://www.youtube.com/watch?v=sUHDW1HhlXY)`

`To flash Ubuntu to emmc: (reference http://com.odroid.com/sigong/prev_forum ... -emmc.html)`  
`7. Copy the Ubuntu compressed image to a USB-hard disk drive from on of these links:`  
`http://odroid.com/dokuwiki/doku.php?id= ... nux_ubuntu (I was not able to extract these files with my MAC)`  
`http://odroid.in/ubuntu_14.04lts/`   
`8. Extract the compressed file on the same USB-HDD (You can download XZ Utils for your MAC http://tukaani.org/xz/)`  
`9. You have to run your odroid with Ubuntu, so flash your SD card using the Wind32disk imager for odroid (I did this from my PC)`  
`10. Boot`   
`11. Change the jumper to SD boot and boot up with your new SDCARD with Ubuntu on it.`  
`12. Check if Ubuntu booted! If so, continue, otherwise double check steps above.`  
`13. Power off the board, reconnect the SDCard to your PC`   
`14. Connect the eMMC with Android as well the SdCard with Ubuntu, set the jumper to SDCard boot.`  
`15. Connect your USB-HDD to the Odroid XU4`  
`16. Boot on your Ubuntu, Open a Terminal and navigate to where you saved your Ubuntu img on the USB-HDD`  
`17. Now figure out wheres your eMMC. Type`  
`ls /dev/mmcblk*`  
`Your eMMC will be the device with with boot0/boot1 on it as well p1/p2/p3/p4 as well. We'll assume that is mmcblk0! (you can also go to /dev/disk/by-id/ and find it there)`  
`18. On the terminal at the folder that your Ubuntu img (your USB-HDD) type:`   
`sudo dd if=ubuntu-14.04.1lts-lubuntu-odroid-xu3-20150212.img of=/dev/mmcblk0 bs=4M conv=fsync`  
`19. It will ask for sudo user and password/ odroid, and then you will see all the capacity of the files transferred.`  
`19. poweroff`  
`17. Remove SDcard and set the jumper to eMMC boot.`  
`18. That is it.` 

## *Temperature*

`sudo armbianmonitor -M`