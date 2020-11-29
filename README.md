# php-docker Beta
These files provide Docker support with a basic PHP application.
The focus is to run OctoberCMS in an Apache environment.

It provide an APACHE server runing PHP (port 8080) - MySql 5.7 - PHPMyAdmin (port 8081)

## Building
Build and run the Docker image:
```
docker-compose up --build
```

Or, just build the Docker image:
```
docker build -f Dockerfile -t php-alone .
```

When your Docker image has been built, run:
```
docker-compose up
```

## Mail settings
To use the mail tester, change the "Mail method" to SMTP
```
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
