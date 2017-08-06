# Networks

In order to avoid IP addressing conflicts as we bring swarm networks up/down, we will statically address each docker overlay network, and record the details below:

Network  | Range
--|--
[Traefik](https://geek-cookbook.funkypenguin.co.nz/ha-docker-swarm/traefik/)  | _unspecified_
[Mail Server](https://geek-cookbook.funkypenguin.co.nz/recipies/mail/)  | 172.16.1.0/24
[Gitlab](https://geek-cookbook.funkypenguin.co.nz/recipies/gitlab/) | 172.16.2.0/24
[Wekan](https://geek-cookbook.funkypenguin.co.nz/recipies/wekan/)  |  172.16.3.0/24
[Piwik](https://geek-cookbook.funkypenguin.co.nz/recipies/piwki/)  |  172.16.4.0/24
[Tiny Tiny RSS](https://geek-cookbook.funkypenguin.co.nz/recipies/tiny-tiny-rss/)  |  172.16.5.0/24
[Huginn](https://geek-cookbook.funkypenguin.co.nz/recipies/huginn/)  |  172.16.6.0/24
