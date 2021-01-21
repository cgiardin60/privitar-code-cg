# SystemD units for privitar components

At the moment, services are provided for the following components:

- Privitar Publisher - privitar-publisher.service
- Publisher-on-demand - privitar-pod.service 

# privitar-publisher.service
This service makes use of the startup.sh and shutdown.sh scriptd distributed with Privitar Publisher. 
SystemD will track the PID of the java process, not that of the script.

# privitar-publisher@.service
This service allows one to start several instances of the Policy Manager by passing a parameter to the service name. 
The instances need to be configured in such a way that the used ports do not clash. It also shows an example of how to establish a dependency on a locally running postgresql server.

# privitar-pod.service 
This service launches a PoD instance directly as a java process. No wrappers are used.

# privitar-pod@.service 
This service allows one to start several instances of the PoD by passing the port as a parameter to the service name.
For example, running:
``` shell
$ sudo systemctl start privitar-pod@8081
$ sudo systemctl start privitar-pod@8082
```
would start two instances of PoD on port 8081 and port 8082. The remaining settings held in the `application.properties` file are honored.

# Installing the service files
To install the service files copy them to the /etc/systemd/system folder and run the following (as root or via sudo)

``` shell
$ systemctl daemon-reload
```

To have these services start at boot time:

``` shell
$ systemctl enable service_file_name
```

# Starting and stopping services
To start, stop, restart or get the status of the service just run (as root or via sudo):

``` shell 
$ systemctl start/stop/restart/status service_file_name
```

# Logging
logs can be found using journalctl

``` shell
$ journalctl -e -u service_file_name
```
