[mux_overview]: https://github.com/remoteit/netmuxdemux/blob/master/docs/muxer-overview.png "mux verview"

# Muxer
Muxer is the initiator/host side of the connection.  Muxer accepts socket connections and send them to the target Demuxer.

![alt text][mux_overview]

In the above example TCP ports 22 and 80, along with UDP port 161 are forwarded to the demuxer target via remote.it

## muxer command format
muxer [-h] [-v(erbose)] [-d][optinal pid file] [-f config_file][-u user_2_run_as] [-t <target demux ip:port>] <bind/listen port list> 

* -h produces help output
* -v produces verbose output, adding a second -v produces debug output also
* -d runs the program as a daemon (unix only)
* -p creates the specified pid file if run as daemon (unix only)
* -u drop privlages to this user when damonized (unix only, defaults to nobody)
* -f use configuration file before parsing command line options
* -t demuxer target ip and port (defaults to 127.0.0.1:5999 if not specified)

Following the command options is the bind/listen list of sockets to accept traffic from and their target ports.  Each entry is
in the following format:

```
[protocol U or T][listen port][:optional target port]
```

#### Special Control Connection
By default demuxer runs a control connnection on its internal TCP port 1 (also configurable by demuxer config).  This control connection can give data on what is happing on the demuxer side, like a connection could not be made on the peer.

To configure this just add a configuration to attach to demuxer control port like so:

T1
-or-
T10000:1

Then you can attach to this socket to get real time data on demuxer.

#### Example TCP port 80 targeting port 8080 demuxer side
```
T80:8080
```

#### Example TCP port 80 targeting port 80 demuxer side
```
T80
```

#### Example UDP port 5000 targeting port 5000 demuxer side
```
U5000
```

#### Example UDP port 5000 targeting port 3333 demuxwer side
```
T5000:3333
```

#### Example sending TCP port 80 and 443 and local UDP port 3845 to 3800 demuxer side
```
T80 T443 U3845:3800
```

#### Full Eample:
```
muxer -v T80 T443 U3845:3800
```
#### Full Eample with non default muxer target:
```
muxer -v -t 127.0.0.2:5998 T80 T443 U3845:3800
```
or with a hostname 
```
muxer -v -t remoteit.local:5998 T80 T443 U3845:3800
```

### Muxer configuration file
The muxer configuration file is parsed before any command line arguments.  Command line arguments will override configuration file options.

### Sample Muxer Configuration File
```
# this is a comment, any line that starts with '#' is a comment and will be ignored.
#
#target demuxer address
target_host 127.0.0.2
target_port 5998

#verbose level 0,1,2
verbose 2

#if daemon, user to run as
#run_as_user nobody 
run_as_user mike 

# sockets to bind
socket_list T2223:22 T8080:80 T2229

#IP to bind to
bind_ip 127.0.0.1
```





