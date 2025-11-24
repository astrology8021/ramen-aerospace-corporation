# access-denied after setting local_hosts

## solutions

1. connect to the container via a terminal
2. edit the config/sabnzbd.ini file

- you may need to install a text editor in the container

3. change value of local_hosts to `local_hosts =  ,`

- there should be a "sabnzbd.ini.bak" in the same folder, try copying these values over
- or destroy the containers (not the volumes) and redeploy them, this should restore the ini to default

# media doesn't auto download on request + approve

- jellyseer and arrs need to be on same network
  - if in another user defined network and the arrs are under gluetun, jellyseer needs to be under gluetun as well
- media needs to not be monitored or radarr/sonarr already for it to download, it needs to add then download
