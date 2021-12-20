# Docker Apache, PHP 7.4, and local HTTPS support

This template is inspired by  https://github.com/craigbuckler/docker-php73

This project can execute a PHP site in any folder from <https://localhost/>.
But the apache configuration is available in the *000-default.conf* file to support domain names. 

It builds a Docker image with SSL, Apache, and PHP 7.4. Port 80 can still be used, but a real SSL certificate avoids development anomalies (such as files not caching in the browser) and prevents port 80 clashes with applications such as Skype.


## Requirements

1. [Docker](https://www.docker.com/) for Windows, macOS, or Linux
1. [mkcert](https://github.com/FiloSottile/mkcert) for creating locally-trusted development SSL certificates ([builds available](https://github.com/FiloSottile/mkcert/releases))

On Mac you can install Mkcert with :
```
$ brew install mkcert
```

## Generate SSL certificates

These steps need only be followed once.

> On Windows devices with WSL2, certificates generated in Windows will work in Linux and vice-versa.

Install a new local certificate authority in your browsers:

```sh
mkcert -install
```

> If this fails in Firefox:
>
> 1. Locate the generated `rootCA.pem` file. It will be at the location returned by entering `mkcert -CAROOT` (Usually `C:\Users\<name>\AppData\Local\mkcert` on Windows).
> 1. In Firefox, open the menu and choose *Options*, then *Privacy & Security*. Scroll to the bottom and click **View Certificates**. Select the **Authorities tab**, click **Import...**, open the `rootCA.pem` file, and restart the browser.

Create locally-trusted development certificates:

```sh
mkcert localhost 127.0.0.1 ::1
```

> You can use any domain, although 'localhost' may be practical when creating Progressive Web Apps or debugging.

Rename the generated files:

* `cert.pem` for the SSL certificate, and
* `cert-key.pem` for the SSL certificate key file

and copy them to the `ssl` directory in this project.

> You can use this certificates in any other project ( with localhost or the same dev domain ). 

**Be sure to .gitignore certificates !** ( see .gitignore files )

## Launch the container with Docker Compose

Alternatively, copy `docker-compose.yml` to your application directory and launch the site with:

```sh
docker-compose up
```

To stop, enter `docker-compose down` in another terminal.
