# Docker Image for XRDP, by [FEROX](https://ferox.yt)

![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/frxyt/xrdp.svg)
![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/frxyt/xrdp.svg)
![Docker Pulls](https://img.shields.io/docker/pulls/frxyt/xrdp.svg)
![GitHub issues](https://img.shields.io/github/issues/frxyt/docker-xrdp.svg)
![GitHub last commit](https://img.shields.io/github/last-commit/frxyt/docker-xrdp.svg)

This image packages XRDP and VNC.

* Docker Hub: https://hub.docker.com/r/frxyt/xrdp
* GitHub: https://github.com/frxyt/docker-xrdp

## Docker Hub Image

**`frxyt/xrdp`**

### Supported tags

* **`frxyt/xrdp:cinnamon`**: with [Cinnamon](http://developer.linuxmint.com/projects/cinnamon-projects.html)
* ~~**`frxyt/xrdp:gnome`**: with [GNOME](https://www.gnome.org/)~~
* ~~**`frxyt/xrdp:kde`**: with [KDE](https://kde.org/)~~
* **`frxyt/xrdp:latest`**: *without any desktop, only XRDP with VNC*
* **`frxyt/xrdp:lxde`**: with [LXDE](https://lxde.org/)
* **`frxyt/xrdp:mate`**: with [MATE](https://mate-desktop.org/)
* **`frxyt/xrdp:xfce`**: with [Xfce](https://www.xfce.org/)

## Usage

### Try it

1. Run an image with a pre-installed desktop:
   * Cinnamon: `docker run --rm -p 33890:3389 frxyt/xrdp:cinnamon`
   * ~~GNOME: `docker run --rm -p 33890:3389 frxyt/xrdp:gnome`~~
   * ~~KDE: `docker run --rm -p 33890:3389 frxyt/xrdp:kde`~~
   * LXDE: `docker run --rm -p 33890:3389 frxyt/xrdp:lxde`
   * MATE: `docker run --rm -p 33890:3389 frxyt/xrdp:mate`
   * Xfce: `docker run --rm -p 33890:3389 frxyt/xrdp:xfce`
1. Start a RDP client:
   * Windows: press `Win+R`, run `mstsc`, connect to: `localhost:33890`
1. Enter default credentials: user `debian`, password `ChangeMe`
1. Enjoy !

### Configurable environment variables

These environment variables can be overriden to change the default behavior of the image and adapt it to your needs:

| Name                     | Default value                                       | Example                                          | Description
| :------------------------| :-------------------------------------------------- | :----------------------------------------------- | :----------
| `FRX_APTGET_DISTUPGRADE` | ` ` *(Empty)*                                       | `1`                                              | Update installed packages
| `FRX_APTGET_INSTALL`     | ` ` *(Empty)*                                       | `midori terminator`                              | Packages to install with `apt-get`
| `FRX_INIT_CMD`           | ` ` *(Empty)*                                       | `echo 'Hello World !'`                           | Command to run before anything else
| `FRX_START_CMD`          | ` ` *(Empty)*                                       | `echo 'Hello World !'`                           | Command to run before starting services
| `FRX_XRDP_CERT_SUBJ`     | `/C=FX/ST=None/L=None/O=None/OU=None/CN=localhost`  | `/C=FR/ST=67/L=SXB/O=FRXYT/OU=IT/CN=xrdp.frx.yt` | XRDP certificate subject
| `FRX_XRDP_USER_NAME`     | `debian`                                            | `john.doe`                                       | Default user name
| `FRX_XRDP_USER_PASSWORD` | `ChangeMe`                                          | `myNOTsecretPassword`                            | Default user password
| `FRX_XRDP_USER_SUDO`     | `1`                                                 | `0`                                              | Add default user to `sudoers` if set to `1`
| `FRX_XRDP_USER_GID`      | `1000`                                              | `33`                                             | Default user ID (UID)
| `FRX_XRDP_USER_UID`      | `1000`                                              | `33`                                             | Default user group ID (GID)
| `FRX_XRDP_USER_COPY_SA`  | `0`                                                 | `1`                                              | Copy default icons to desktop if set to `1`
| `TZ`                     | `Etc/UTC`                                           | `Europe/Paris`                                   | Default time zone

### Example

To run this image, you can use this sample `docker-compose.yml` file:

```yaml
php:
  image: frxyt/xrdp:latest
  environment:
    - FRX_APTGET_INSTALL=task-xfce-desktop
    - FRX_INIT_CMD=echo "startxfce4" > /etc/skel/.xsession
  ports:
    - "22000:22"
    - "3389:3389"
  volumes:
    - ./home:/home:rw
```

### Execute custom scripts upon startup

You can copy your executable scripts in `/frx/entrypoint.d/` and they'll be executed in alphabetical order right before `supervisor` is started.

### Start custom process in background

You can use `supervisor` to start them and place all the services you need as `.conf` files in `/etc/supervisor/conf.d/`.

## Build

```sh
docker build -f Dockerfile -t frxyt/xrdp:latest .
```

## License

This project and images are published under the [MIT License](LICENSE).

```
MIT License

Copyright (c) 2019 FEROX YT EIRL, www.ferox.yt <devops@ferox.yt>
Copyright (c) 2019 Jérémy WALTHER <jeremy.walther@golflima.net>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```