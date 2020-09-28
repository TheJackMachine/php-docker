# php-docker Beta

These files provide Docker support with a basic PHP application.
The focus is to run OctoberCMS in an Apache environment.

It provide an APACHE server runing PHP (port 8080) - MySql 5.7 - PHPMyAdmin (port 8081)

## Instructions
### Usage

#### Method A

Build the image for the PHP server (may take a while)
```
docker build -f Dockerfile -t php-alone .
```

When done, simply run
```
docker-compose up
```

#### Method B

For the first time, run the command with buuild option to create PHP image
```
docker-compose up --build
```

Later, you can juste run :
```
docker-compose up
```




### Mail settings

To use the mail tester switch to SMTP
```
SMTP Address: mailhog
SMTP Port: 1025
SMTP Encryption: No encryption
No username or password, see screenshot.
```

## To test on Windows and Mac

- Case sensitivity
- Files permissions
- Server response time
