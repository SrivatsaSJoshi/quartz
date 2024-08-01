[Tailscale](https://tailscale.com/) is a powerful application based on Wireguard technology which lets us access our machines over the internet as if they were on our network. The communication is decentralized and takes the shortest path between the two computers with tailscale's servers only coming in for initial synchronization.

As powerful as this is, the default installation does not support running on an unprivileged lxc container. The most popular way to run lxc containers is [Proxmox](proxmox.com) which is what I'm using. To set up tailscale on unprivileged containers, follow the steps below.

### Step 1: Install tailscale
Follow the instructions on [Download · Tailscale](https://tailscale.com/download/linux)
It is as simple as running a single shell command but I advice anyone using this to refer to the above link for up to date information
```bash
curl -fsSL https://tailscale.com/install.sh | sh
```
### Step 2:
Open the tailscaled service present in `/usr/lib/systemd/system/tailscaled.service` using a text editor
```bash
nano /usr/lib/systemd/system/tailscaled.service
```

### Step 3:
And change the ExecStart parameter to run tailscaled in usermode
```
ExecStart=/usr/sbin/tailscaled --tun=userspace-networking --socks5-server=localhost:1055 --outbound-http-proxy-listen=localhost:1055
```

### Alternatively, you can copy the complete service and paste it over the default one.

This command will empty the service file
```bash
> /usr/lib/systemd/system/tailscaled.service
```

You can the open the file in a text editor and paste in the below.
```
[Unit]
Description=Tailscale node agent
Documentation=https://tailscale.com/kb/
Wants=network-pre.target
After=network-pre.target NetworkManager.service systemd-resolved.service

[Service]
EnvironmentFile=/etc/default/tailscaled
ExecStart=/usr/sbin/tailscaled --tun=userspace-networking --socks5-server=localhost:1055 --outbound-http-proxy-listen=localhost:1055
ExecStopPost=/usr/sbin/tailscaled --cleanup

Restart=on-failure

RuntimeDirectory=tailscale
RuntimeDirectoryMode=0755
StateDirectory=tailscale
StateDirectoryMode=0700
CacheDirectory=tailscale
CacheDirectoryMode=0750
Type=notify

[Install]
WantedBy=multi-user.target
```

The above will use userspace-networking mode built into tailscale when the service starts up.
## Resources
[Userspace networking mode (for containers) · Tailscale Docs](https://tailscale.com/kb/1112/userspace-networking)

Alternative method (not used here): [Tailscale in LXC containers · Tailscale Docs](https://tailscale.com/kb/1130/lxc-unprivileged)