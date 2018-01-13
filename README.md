# Ubuntu Old Fashioned
![Ubuntu Old Fashioned](ubuntu-old-fashioned.png)

Sometimes you don't want the modern comfort of a distributed build system.

Sometimes just just want to look at a directory and be like "build this now".

Sometimes you don't want to use this scary newfangled "cloud" thing.

Sometimes you're in the mood for something nice and sequential.

Well look no more!

This script is meant to let you build ubuntu cloud images locally from a
livecd-rootfs checkout.

## Installation

On Ubuntu (Xenial):

- sudo add-apt-repository -u ppa:tribaal/oldfashioned
- sudo apt install oldfashioned

## Example

The most simple example to build all ubuntu-cpc images from scratch is:

```bash
bzr co lp:livecd-rootfs
cd livecd-rootfs
sudo old-fashioned-image-build
```

The images will be copied to your $HOME in a "build.output/" folder after about
30 minutes.

## Speeding things up a bit

To speed up package lookup you can install "squid-deb-proxy" on the host, then
point the host to its own proxy by adding a file like the following:

```bash
export LXD_ADDRESS=$(ifconfig lxdbr0 | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}')
cat > /etc/apt/apt.conf.d/30squid-proxy << EOF
Acquire::http::Proxy "http://$LXD_ADDRESS:8000";
EOF
```

The script will autodetect proxy settings as long as they are set in a file in
/etc/apt/apt.conf.d/ .

## Quotes

```
slangasek> "what kind of glass do you serve an ubuntu old fashioned in? a chrisglass"
```
