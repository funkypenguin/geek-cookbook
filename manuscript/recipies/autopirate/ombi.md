!!! warning
    This is not a complete recipe - it's a component of the [AutoPirate](/recipies/autopirate/) "_uber-recipe_", but has been split into its own page to reduce complexity.

# Ombi

[Ombi](https://github.com/tidusjar/Ombi) is a useful addition to the [autopirate](/recipies/autopirate/) stack. Features include:

* Lets users request Movies and TV Shows (_whether it being the entire series, an entire season, or even single episodes._)
* Easily manage your requests
User management system (_supports plex.tv, Emby and local accounts_)
* A landing page that will give you the availability of your Plex/Emby server and also add custom notification text to inform your users of downtime.
* Allows your users to get custom notifications!
* Will show if the request is already on plex or even if it's already monitored.
Automatically updates the status of requests when they are available on Plex/Emby

![Ombi Screenshot](../../images/ombi.png)

## Inclusion into AutoPirate

To include Ombi in your [AutoPirate](/recipies/autopirate/) stack, include the following in your autopirate.yml stack definition file:

````
ombi:
  image: linuxserver/ombi:latest
  env_file : /var/data/config/autopirate/ombi.env
  volumes:
   - /var/data/autopirate/ombi:/config
  networks:
  - internal

ombi_proxy:
  image: a5huynh/oauth2_proxy
  env_file : /var/data/config/autopirate/ombi.env
  networks:
    - internal
    - traefik_public
  deploy:
    labels:
      - traefik.frontend.rule=Host:ombi.example.com
      - traefik.docker.network=traefik_public
      - traefik.port=4180
  volumes:
    - /var/data/config/autopirate/authenticated-emails.txt:/authenticated-emails.txt
  command: |
    -cookie-secure=false
    -upstream=http://ombi:3579
    -redirect-url=https://ombi.example.com
    -http-address=http://0.0.0.0:4180
    -email-domain=example.com
    -provider=github
    -authenticated-emails-file=/authenticated-emails.txt
````

!!! tip
    I share (_with my [patreon patrons](https://www.patreon.com/funkypenguin)_) a private "_premix_" git repository, which includes necessary docker-compose and env files for all published recipes. This means that patrons can launch any recipe with just a ```git pull``` and a ```docker stack deploy``` 👍

## Assemble more tools..

Continue through the list of tools below, adding whichever tools your want to use, and finishing with the **[end](/recipies/autopirate/end/)** section:

* [SABnzbd](/recipies/autopirate/sabnzbd.md)
* [NZBGet](/recipies/autopirate/nzbget.md)
* [RTorrent](/recipies/autopirate/rtorrent/)
* [Sonarr](/recipies/autopirate/sonarr/)
* [Radarr](/recipies/autopirate/radarr/)
* [Mylar](/recipies/autopirate/mylar/)
* [Lazy Librarian](/recipies/autopirate/lazylibrarian/)
* [Headphones](/recipies/autopirate/headphones/)
* [NZBHydra](/recipies/autopirate/nzbhydra/)
* [NZBHydra2](/recipies/autopirate/nzbhydra2/)
* Ombi (this page)
* [Jackett](/recipies/autopirate/jackett/)
* [End](/recipies/autopirate/end/) (launch the stack)


## Chef's Notes 📓

1. In many cases, tools will integrate with each other. I.e., Radarr needs to talk to SABnzbd and NZBHydra, Ombi needs to talk to Radarr, etc. Since each tool runs within the stack under its own name, just refer to each tool by name (i.e. "radarr"), and docker swarm will resolve the name to the appropriate container. You can identify the tool-specific port by looking at the docker-compose service definition.

### Tip your waiter (donate) 👏

Did you receive excellent service? Want to make your waiter happy? (_..and support development of current and future recipes!_) See the [support](/support/) page for (_free or paid)_ ways to say thank you! 👏

### Your comments? 💬
