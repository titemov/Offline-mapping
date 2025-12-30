# Docker installation cheatsheet for offline usage

This cheatsheet will provide basic information about how it can be possible to install Docker on machines, that does not have any internet connection.

## Windows

Tested on Windows 10

Just download [Docker Desktop](https://www.docker.com/products/docker-desktop/) from official website and install for personal use without any account authorization.

## Linux (Ubuntu/Debian)

Tested on [Complete](https://www.debian.org/CD/) version of Debian 13.2.0 "Trixie"

First of all you need to select correct codename of your system on docker packages website:
- [Ubuntu systems](https://download.docker.com/linux/ubuntu/dists/)
- [Debian systems](https://download.docker.com/linux/debian/dists/)

**Download latest version of every package (there will be multiple link to the same packages, but different version)**

>[!NOTE]
> 64 bit systems are called `amd64`

Visit website below 
- Ubuntu - `https://packages.ubuntu.com/<codename>/libs/`
- Debian - `https://packages.debian.org/en/<codename>/allpackages`

To install following dependecies for Docker packages:
1. `iptables`
2. `libc6`
3. `libip4tc2`
4. `libip6tc2`
5. `libmnl0`
6. `libnetfilter-conntrack3`
7. `libnfnetlink0`
8. `libnftnl11`
9. `libxtables12`
10. `netbase`

After that just put all of those `.deb` packages in the same place and run following command

`sudo dpkg --force-depends -i *.deb`

>[!IMPORTANT]
>Make sure that Docker is running by writing `systemctl status docker.service` from `/opt/` directory
