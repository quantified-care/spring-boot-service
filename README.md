# spring-boot-service

Scripts to allow spring boot jars to run as system services in unix

## Installation

Clone the repository into `/opt/spring-boot/` or a custom directory. If using a directory other than the default, change `rootdir` in the `spring-boot-service` script to reflect the change.

Change the group ownership of `rootdir` and its contents to the `www` group or your own custom group
```
sudo chown -R root:www /opt/spring-boot
```

Change the directory permissions of `rootdir` and its subdirectories to add group write permissions and to set the group ID on future subdirectories
```
sudo chmod 2775 /opt/spring-boot
find /opt/spring-boot -type d -exec sudo chmod 2775 {} +
```

Recursively change the file permissions of `rootdir` and its subdirectories to add group write permissions
```
find /opt/spring-boot -type f -exec sudo chmod 0664 {} +
```
Change the execute permission for the service init script
```
sudo chmod 755 /opt/spring-boot/spring-boot-service
```

## Adding a service

Create directories for the service in the `apps` and `logs` subdirectories with the same name as the service. Extract the application jar and conf file into the app directory.

Create a link to the service in `/etc/init.d/`
```
ln -s /opt/spring-boot/spring-boot-service /etc/init.d/my-service
```

## Running a service

Installed services can be run and stopped just like any system service
```
sudo service my-service start
sudo service my-service status
sudo service my-service stop
```
