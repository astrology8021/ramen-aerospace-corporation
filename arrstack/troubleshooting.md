# can't connect radarr, sonarr, lidarr to sabnzbd

- need to have any arr app/container on the same userspace as sabnzbd
- sabnzbd is on the gluetun userspace, the other arr apps may be under a compose defined network userspace, therefore they can't communicate

## solution

- add the ports to gluetun
  this joins containers to the same userspace
- this now puts those containers behind the VPN

### sources

- https://www.reddit.com/r/radarr/comments/17nbevl/configuring_gluetun_container_with_piaradarr_on_a/
- https://www.reddit.com/r/selfhosted/comments/1gtp803/arr_apps_competing_for_the_same_port_when_using/

# can't connect prowlarr to sabnzbd

1. click status and interface options (spanner icon)
2. get local ipv4 address

- Use this as the IP when adding in prowlarr as the download client

## possible other contributing solutions

- add container names to whitelist: https://forum.yams.media/viewtopic.php?t=159

### sources

- https://www.reddit.com/r/radarr/comments/o9pk5u/radarr_wont_connect_to_sabnzbd_with_identical/

# nginx proxy manager won't resolve

## solution

Set the proxy pass to 0.0.0.0 for any host instead of local host

- Scheme: http
- Settings icon (Custom Nginx Configuration)

```
   location /sabnzbd {
 proxy_pass http://0.0.0.0:8085;
 proxy_set_header Host $host;
 proxy_set_header X-Real-IP $remote_addr;
 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
 auth_basic "Restricted Content";
 auth_basic_user_file ..\.htpasswd;

}
```

If needed, edit the sabnzbd.ini file inside the container if you need to add a password or add whitelisted hosts

1. start a terminal in the container
   `docker exec -it sabnzbd bash`
2. install nano or vim - Used the "lscr.io/linuxserver/sabnzbd" image so yours may be different, Alpine based image:
   `apk add nano`
3. Edit the config file
   `nano config/sabnzbd.ini`

### sources

> superkoning
>
> > Your Sabnzbd Host says "127.0.0.1". Which is techno talk for "localhost". Change it to 0.0.0.0, Save, and restart SABnzbd, and you should be OK.

[Can't access SabNZBD on my network](https://www.reddit.com/r/SABnzbd/comments/1g8znlm/cant_access_sabnzbd_on_my_network/)

```
}
location ^~ /sabnzbd {
proxy_pass http://localhost:8080;
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
auth_basic "Restricted Content";
auth_basic_user_file ..\.htpasswd;
}
```

[Timeouts when accessing SABnzbd via nginx reverse proxy](https://www.reddit.com/r/SABnzbd/comments/7575c4/timeouts_when_accessing_sabnzbd_via_nginx_reverse/)

#### Other sources

- [Can't access via domain](https://www.reddit.com/r/SABnzbd/comments/1hr6awr/cant_access_via_domain/)
