# consul

For more details, please read Document:

[consul get-start](https://www.consul.io/intro/getting-started/install.html)

[consul Docs](https://www.consul.io/docs/index.html)



Below is short guide for using consul

Download, depend on your own system type:

[https://www.consul.io/downloads.html](https://www.consul.io/downloads.html)

Permanently set $PATH on Linux/Unix:

```text
#You need to add it to your ~/.profile or ~/.bashrc file. 
export PATH="$PATH:/path/to/dir"

#Depending on what you're doing, you also may want to symlink to binaries:
cd /usr/bin
sudo ln -s /path/to/binary binary-name

#Note that this will not automatically update your path for the remainder of the session. To do this, you should run:
source ~/.profile 
#or
source ~/.bashrc
```

Run Agent \(test\)

```text
consul agent -dev   #leave this running 
```

open an other terminal 

[consul members](https://www.consul.io/docs/commands/members.html)

```text
consul members
consul members -detailed
consul members -http-addr=localhost:8500  
```

check on website

`curl localhost:8500/v1/catalog/nodes` 

close

Ctrl+C or ps & kill



* run agent: consul agent -dev 
* join to  group : consul join \[IP\] [consul join](https://www.consul.io/docs/commands/join.html)
* list all members: consul members 
* leave group: consul leave  [consul leave](https://www.consul.io/docs/commands/leave.html)

[consul CLI](https://www.consul.io/docs/commands/index.html)

```text
$ consul
Usage: consul [--version] [--help] <command> [<args>]

# means only new version have this function
Available commands are:
    agent          Runs a Consul agent
    #catalog        Interact with the catalog
    #connect        Interact with Consul Connect
    event          Fire a new event
    exec           Executes a command on Consul nodes
    force-leave    Forces a member of the cluster to enter the "left" state
    info           Provides debugging information for operators.
    #intention      Interact with Connect service intentions
    join           Tell Consul agent to join cluster
    keygen         Generates a new encryption key
    keyring        Manages gossip layer encryption keys
    kv             Interact with the key-value store
    leave          Gracefully leaves the Consul cluster and shuts down
    lock           Execute a command holding a lock
    maint          Controls node or service maintenance mode
    members        Lists the members of a Consul cluster
    monitor        Stream logs from a Consul agent
    operator       Provides cluster-level tools for Consul operators
    reload         Triggers the agent to reload configuration files
    rtt            Estimates network round trip time between nodes
    #services       Interact with services
    snapshot       Saves, restores and inspects snapshots of Consul server state
    validate       Validate config files/directories
    version        Prints the Consul version
    watch          Watch for changes in Consul
```

[consul agent -- Options](https://www.consul.io/docs/agent/options.html)

```text
consul agent -h
==> Usage: consul agent [options]

  Starts the Consul agent and runs until an interrupt is received. The
  agent represents a single node in a cluster.

 Command Options

  -advertise=<string>
     Sets the advertise address to use.

  -advertise-wan=<string>
     Sets address to advertise on WAN instead of -advertise address.

  -atlas=<string>
     (deprecated) Sets the Atlas infrastructure name, enables SCADA.

  -atlas-endpoint=<string>
     (deprecated) The address of the endpoint for Atlas integration.

  -atlas-join
     (deprecated) Enables auto-joining the Atlas cluster.

  -atlas-token=<string>
     (deprecated) Provides the Atlas API token.

  -bind=<string>
     Sets the bind address for cluster communication.

  -bootstrap
     Sets server to bootstrap mode.

  -bootstrap-expect=<int>
     Sets server to expect bootstrap mode.

  -client=<string>
     Sets the address to bind for client access. This includes RPC, DNS,
     HTTP and HTTPS (if configured).

  -config-dir=<value>
     Path to a directory to read configuration files from. This
     will read every file ending in '.json' as configuration in this
     directory in alphabetical order. This can be specified multiple
     times.

  -config-file=<value>
     Path to a JSON file to read configuration from. This can be
     specified multiple times.

  -data-dir=<string>
     Path to a data directory to store agent state.

  -dc=<string>
     Datacenter of the agent (deprecated: use 'datacenter' instead).

  -dev
     Starts the agent in development mode.

  -disable-host-node-id
     Setting this to true will prevent Consul from using information
     from the host to generate a node ID, and will cause Consul to
     generate a random node ID instead.

  -dns-port=<int>
     DNS port to use.

  -domain=<string>
     Domain to use for DNS interface.

  -encrypt=<string>
     Provides the gossip encryption key.

  -http-port=<int>
     Sets the HTTP API port to listen on.

  -join=<value>
     Address of an agent to join at start time. Can be specified
     multiple times.

  -join-wan=<value>
     Address of an agent to join -wan at start time. Can be specified
     multiple times.

  -log-level=<string>
     Log level of the agent.

  -node=<string>
     Name of this node. Must be unique in the cluster.

  -node-id=<string>
     A unique ID for this node across space and time. Defaults to a
     randomly-generated ID that persists in the data-dir.

  -node-meta=<key:value>
     An arbitrary metadata key/value pair for this node, of the format
     `key:value`. Can be specified multiple times.

  -non-voting-server
     (Enterprise-only) This flag is used to make the server not
     participate in the Raft quorum, and have it only receive the data
     replication stream. This can be used to add read scalability to
     a cluster in cases where a high volume of reads to servers are
     needed.

  -pid-file=<string>
     Path to file to store agent PID.

  -protocol=<int>
     Sets the protocol version. Defaults to latest.

  -raft-protocol=<int>
     Sets the Raft protocol version. Defaults to latest.

  -recursor=<value>
     Address of an upstream DNS server. Can be specified multiple times.

  -rejoin
     Ignores a previous leave and attempts to rejoin the cluster.

  -retry-interval=<string>
     Time to wait between join attempts.

  -retry-interval-wan=<string>
     Time to wait between join -wan attempts.

  -retry-join=<value>
     Address of an agent to join at start time with retries enabled. Can
     be specified multiple times.

  -retry-join-ec2-region=<string>
     EC2 Region to discover servers in.

  -retry-join-ec2-tag-key=<string>
     EC2 tag key to filter on for server discovery.

  -retry-join-ec2-tag-value=<string>
     EC2 tag value to filter on for server discovery.

  -retry-join-gce-credentials-file=<string>
     Path to credentials JSON file to use with Google Compute Engine.

  -retry-join-gce-project-name=<string>
     Google Compute Engine project to discover servers in.

  -retry-join-gce-tag-value=<string>
     Google Compute Engine tag value to filter on for server discovery.

  -retry-join-gce-zone-pattern=<string>
     Google Compute Engine region or zone to discover servers in (regex
     pattern).

  -retry-join-wan=<value>
     Address of an agent to join -wan at start time with retries
     enabled. Can be specified multiple times.

  -retry-max=<int>
     Maximum number of join attempts. Defaults to 0, which will retry
     indefinitely.

  -retry-max-wan=<int>
     Maximum number of join -wan attempts. Defaults to 0, which will
     retry indefinitely.

  -serf-lan-bind=<string>
     Address to bind Serf LAN listeners to.

  -serf-wan-bind=<string>
     Address to bind Serf WAN listeners to.

  -server
     Switches agent to server mode.

  -syslog
     Enables logging to syslog.

  -ui
     Enables the built-in static web UI server.

  -ui-dir=<string>
     Path to directory containing the web UI resources.

```



Blueking consul analysis

```text
/usr/bin/consul agent -config-file=/data/bkee_zkl/etc/consul.conf -config-dir=/data/bkee_zkl/etc/consul.d
```



/etc/consul.conf

```text

{
   “rejoin_after_leave”: true,
   “skip_leave_on_interrupt”: true,
   “recursors”: [
       “183.60.83.19",
       “183.60.82.98”
   ],
    #current internal IP
   “bind_addr”: “10.38.0.7”,
   #can change
   “node_id”: “1cb57f74-1c82-4eac-be95-8d90607d04c7”,
   #join consul server
   “retry_join”: [
       “10.38.0.4”,
       “10.38.0.7",
       “10.38.0.13”
   ],
   “log_level”: “info”,
   #define whether current is used as consul server/client
   “server”: true,
   #use same dc in one game branch
   “datacenter”: “dc2",
   #one game one dir 
   “data_dir”: “/tmp/consul_tmp/“,
   “leave_on_terminate”: false,
   #can change to any name, but usually can use hostname 
   “node_name”: “t07”,
   #define pid 
   “pid_file”: “/etc/consul2.d/consul.pid”,
   # temp delete line:  “bootstrap_expect”: 3,
   “encrypt”: “V6lKBir7Kl08GceMhxm1wg==“,
   #these port must define when we need different instance
   “ports”: {
       “dns”: 1053, #default 53
       “server”:9300, #default 8300
       “serf_lan”:9301, #default 8301
       “serf_wan”:9302, #default 8302
       “http”:9500 #default 8500
   }
}

```



