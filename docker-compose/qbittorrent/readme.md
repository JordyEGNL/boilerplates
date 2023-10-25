# qBittorrent with Gluetun

## Requirements
- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/)
- Active VPN provider that supports OpenVPN or WireGuard

## Guide
1. First you need to check if your VPN provider is compatible with Gluetun
https://github.com/qdm12/gluetun-wiki/tree/main/setup/providers

I am using Mullvad with OpenVPN so I need to use the 'VPN_SERVICE_PROVIDER=mullvad' and 'OPENVPN_USER=xxxx' variables

2. Edit the docker-compose.yml file to your needs. The standard config is for Mullvad

If you want to add more containers to the mullvad vpn, do NOT create a second Mullvad container, as this adds one device to your device limit (5 as of now). Instead add it to the docker-compose stack and add this line to the container service.
```yml
network_mode: "service:gluetun"
```

You will also need to publish the correct ports in the Gluetun container if you want to access the containers from outside. Just like I did for qBittorrent
```yml
    ports:
      - 6881:6881
      - 6881:6881/udp
      - 8085:8085
```

3. Deploy the docker-compose.yml file and see live logs from the stack
```bash
sudo docker compose up -d && docker compose logs -f
```

After some time you should see something similar to this
```log
2023-10-25T14:48:15Z INFO [dns] ready
2023-10-25T14:48:16Z INFO [ip getter] Public IP address is x.x.x.x
2023-10-25T14:48:16Z INFO [vpn] You are running on the bleeding edge of latest!
```

You can also check if qBittorrent is correctly connected with the following command
```bash
docker exec qbittorrent curl ifconfig.me
```

This should respond with your VPN ip. If your real IP is still shown, the VPN is not working correctly