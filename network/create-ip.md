
# Create IP address on solaris

- ip v4 is configured as follow

```
# ipadm create-ip net0
# ipadm create-addr -T static -a local=10.9.8.7/24 net0
net0/v4
```

- ip v6 is configured as follow

```
# ipadm create-ip net0
# ipadm create-addr -T addrconf net0
net0/v6
# ipadm create-addr -T static -a local=ec0:a:99:18:209:3dff:fe00:4b8c/64 net0
net0/v6a
```

- Configure an interface as follow

```
# ipadm create-ip net0
# ipadm create-addr -T dhcp net0
net0/v6a
```

- Use the addrconf argument with the –T option to specify an automatically generated IPv6 address:

```
# ipadm create-ip net0
# ipadm create-addr -T addrconf net0
net0/v6
```

- If you wanted to change the IP address that was provided for the net0 interface in the previous example, you would need to first remove the interface and then re-add it, as shown in the following example:

```
# ipadm delete-addr net0/v4
# ipadm create-addr -T static -a local=10.7.8.9/24 net0
net0/v4
```

- Configure persistent Routes
- Because the /etc/defaultrouter file is deprecated in Oracle Solaris 11, you can no longer manage routes (default or otherwise) by using this file. Using the route command is the only way that you can manually add a route to a system. To make the changes persistent across reboots, use the –p option with the route command

```
# route -p  add default ip-address
```

- For example, you would add a route to network 10.0.5.0, which has its gateway as the border router, as follows:

```
# route -p add -net 10.0.5.0/24 -gateway 10.0.5.150
add net 10.0.5.0: gateway 10.0.5.150
```

- View routes that were created by the using the previous command as follows:

```
# route -p show
```

- Also, note that after an installation, you can no longer determine a system's default route by checking the /etc/defaultrouter file. To display the currently active routes on a system, use the netstat command with the following options:

```
# netstat -rn
```
