[demux_overview]: https://github.com/remoteit/netmuxdemux/blob/master/docs/demux-overview.png "demux overview"

# Demuxer
Demxer is the target software that accepts connections from Muxer on a single TCP port and creates the requested TCP and UDP sockets to the specfied target.

!["demux overview"][demux_overview]

## Build

Build can be done with the make file in the src directory for unix, or either windows dev studio 2010 or 2017. This project can also build with the buildall script in the root directory that builds all archtectures in available in the tools directory.

## demux command format
demux [-h][-v(erbose)][-f config_file][-d][-p pidfile][-u user_2_run_as][-b <bindip:port>][-e <udp_expire_time>][-t <target_host>]

* -h produces help output
* -v produces verbose output, adding a second -v produces debug output also
* -f use configuration file before parsing command line options
* -d run as daemon (non windows only)
* -p generate specified pidfile if daemon (non windows only)
* -u user to run as as (non windows only, must start as root, drop privs to this user)
* -b bind/listen on ip:port (default 127.0.0.1:5999)
* -e udp expire time in seconds (default 120)
* -t target_host (default 127.0.0.1)

## Listen IP:Port
The Demuxer will listen on an IP:Port for connections from the muxer (default 127.0.0.1:5999).  Typically this will be through a remote.it connection.   A remote.it service will target the Dexmuxer listen IP:Port.

## Target host
The Demux Target Host is the host that all connections will target. The target host by default is 127.0.0.1, the taret host can be overridden with the -t option.  Either an IP address or a resolvable hostname can be used for the target host.

Muxer will map ports from its side which will be in listen mode to ports on the target host which also should be in listen mode for TCP and bound for UDP.





