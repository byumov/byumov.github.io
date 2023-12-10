---
title: "Wireguard с UI"
date: 2023-12-10T18:13:44+03:00
draft: false
---

Простой способ поднять [wireguard](https://www.wireguard.com/) с UI в одну команду:

```bash
export PASS="<password>"

podman run -d \
    --name=wg \
    -e WG_HOST=135.181.42.186 \
    -e PASSWORD=$PASS \
    -v ~/.wg-easy:/etc/wireguard \
    -p 51820:51820/udp \
    -p 51821:51821/tcp \
    --cap-add=NET_ADMIN \
    --cap-add=SYS_MODULE \
    --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
    --sysctl="net.ipv4.ip_forward=1" \
    --restart unless-stopped \
    weejewel/wg-easy
```

[https://github.com/wg-easy/wg-easy](https://github.com/wg-easy/wg-easy)
