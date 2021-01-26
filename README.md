# traefik-seedbox

Plex media server and rtorrent-flood with traefik in docker and docker-compose

## Installation

Clone the repo
```Shell
$ git clone https://github.com/a-pichard/traefik-seedbox.git
$ cd traefik-seedbox
$ mkdir flood-db && mkdir storage && mkdir -p plex/config && mkdir -p plex/transcode
```

In `docker-compose.yml`  and all of the dynamic configuration files replace all `domain.com` by your desired domain.

In `dynamic/middlewares.yml` replace `user:hashed-password` by the user/hashed-password you want (https://doc.traefik.io/traefik/middlewares/basicauth/)

Get a claim token: https://plex.tv/claim and replace in `docker-compose.yml` 

`- PLEX_CLAIM=claim-xxx....`

/!\ important if you want Plex Apps to access your server remotely:

Make sure to replace the env variable value `ADVERTISE_IP=https://<plex.domain.com>:443` with your desired domain.

Run it now

```Shell
$ docker-compose up -d
```

```Shell
$ sudo chown -R $USER * # or chown only created folders recursively 
```

Then

Go to `https://plex.domain.com/web` and follow plex installation.

If you have the `No soup for you` error you need to make the configuration locally (or SSH tunnel).
```Shell
$ ssh -L 8888:127.0.0.1:32400 user@plex.domain.com
```
And start the configuration on `localhost:8888/web`

Enable remote access during installation

## Enjoy

### Credits for the Plex configuration
[pierre-emmanuelJ/plex-traefik](https://github.com/pierre-emmanuelJ/plex-traefik)
