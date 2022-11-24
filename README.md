# PXE Server

## Configuration

* Drop .iso files in `./volumes/isos/`
* Extract from those ISOs the kernel (usually `vmlinuz` or `linux`) and the initrd (usually `initrd.gz` or `initrd.lz`) and drop them at `./volumes/files/`
  * Each .iso could have its own folder at `./volumes/files/` to organize the kernel and initrd files
* Edit `./volumes/tftpboot/pxelinux.cfg/distros` to add the distro you want to configure. Each distro has a different way of being called, some online research might be necessary. You can look at the [syslinux official documentation](https://wiki.syslinux.org/wiki/index.php?title=Config) to check the options available.
* Configure a static ip in your network interface. For example: 10.0.0.1/24
* Edit `docker-compose.yml`, the `command: ` options are passed to `dnsmasq`. Configure the network with the configuration you want. You can look at the [dnsmasq official documentation](https://thekelleys.org.uk/dnsmasq/docs/dnsmasq-man.html) for other arguments.
  * Remember to change `enp6s0` with the name of your network interface
* Make sure port 53 and 80 are not being used
* Run `docker-compose build && docker-compose pull` to prepare the images

## Launch server

```bash
docker-compose up -d
```
