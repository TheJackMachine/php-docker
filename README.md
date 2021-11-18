# php-docker Beta

These files provide Docker support with a basic PHP application.
The focus is to run OctoberCMS in an Apache environment.

It provide an APACHE server runing PHP (port 8080) - MySql 5.7 - PHPMyAdmin (port 8081)

## Versions

Choose between `php5.6-mcrypt`, `php7.2-mcrypt` or `php7.3`, then copy those files at the root of your project folder.
If you are using an Apple Silicon Mac, you can use the files in `apple-silicon`. Support for mailhog has been temporarily removed until a solution has been found.

## Building

Build and run the Docker image:

```bash
docker-compose up --build
```

Or, just build the Docker image:

```bash
docker build -f Dockerfile -t php-alone .
```

When your Docker image has been built, run:

```bash
docker-compose up
```

## MySQL settings

Uncomment lines 30-31 and 51-52 in `docker-compose.yaml` to enable persistent mysql data.

Docker will create the volume for you in the `/var/lib/docker/volumes` folder. This volume persist as long as you are not typing:

```bash
docker-compose down -v
```

## PHPMyAdmin settings

Uncomment lines 41-42 in `docker-compose.yaml` to skip phpmyadmin login screen.

## Mail settings

To use the mail tester, change the "Mail method" to SMTP

```text
SMTP Address: mailhog
SMTP Port: 1025
SMTP Encryption: No encryption
No username or password, see screenshot.
```

![OctoberCMS Screenshot](https://github.com/TheJackMachine/php-docker/blob/master/mailsettings.jpg)

## To test on Windows and Mac

- Case sensitivity
- Files permissions
- Server response time
