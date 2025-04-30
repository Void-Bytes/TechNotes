## Setup Shell Commands

### Binding to specific ports and host names

Set **ASPNETCORE_URLS** environment variable (semi-colon separated, wildcards supported):
```bash
export ASPNETCORE_URLS="http://*:28001"
```

**As root, redirect incoming port 80 connections to application port**:
```bash
# Access CLI as root
su

# Make sure iptables is installed
apk update
apk upgrade
apk add iptables

# Route port 80 to application port (eg: 28001)
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 28001

# View existing rules
iptables -t nat --line-numbers -n -L

# Delete a rule by number
iptables -t nat -D PREROUTING 2
```
## Registering as a Service

Create OpenRC initialization script for service, example location: "/etc/init.d/your_service_name"
```
#!/sbin/openrc-run
# The name of the service
name="your_service_name"

# The command to start your service
command="/path/to/your/service"

# The pid file of your service
pidfile="/var/run/your_service.pid"

# Required dependencies for your service
depend() {
    need net
}

# Start the service
start() {
    ebegin "Starting your service"
    # Start your service in the background
    start-stop-daemon --start --background --pidfile $pidfile --make-pidfile --exec $command
    eend $?
}

# Stop the service
stop() {
    ebegin "Stopping your service"
    # Kill the service using the pid file
    start-stop-daemon --stop --pidfile $pidfile
    eend $?
}
```

Make the script executable:
```bash
chmod +x /etc/init.d/your_service_name
```

Add the service to the default run level:
```bash
rc-update add your_service_name default
```

Test the service:
```bash
/etc/init.d/your_service_name start
/etc/init.d/your_service_name stop
```