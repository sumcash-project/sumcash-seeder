# sumcoin-seeder


## Sumcoin-seeder is a crawler for the Sumcoin network, which exposes a list
of reliable nodes via a built-in DNS server.

### Features:

* regularly revisits known nodes to check their availability

* bans nodes after enough failures, or bad behavior

* accepts nodes down to v0.5.0 to request new IP addresses from,
  but only reports good post-v0.6.9 nodes.
* keeps statistics over (exponential) windows of 2 hours, 8 hours,

  1 day and 1 week, to base decisions on.
* very low memory (a few tens of megabytes) and cpu requirements.

* crawlers run in parallel (by default 96 threads simultaneously).

### Install the dependencies

```
sudo apt-get install build-essential libboost-all-dev libssl-dev
```

### Clone the project

First, you'll need a droplet with a domain assigned to it. Once that is set up, you can start on the actual seeder.

First, go into the digital ocean panel (or whichever service you use) for the domain. Add a new NS record, making the hostname something like "dnsseed" and directed to the IP of the droplet. Once that's done, log into the droplet as root. Download the seeder with ...

```
git clone https://github.com/sumcoinlabs/sumcoin-seeder.git"
```


### USAGE
-----

Assuming you want to run a dns seed on dnsseed.example.com, you will
need an authorative NS record in example.com's domain record, pointing
to for example vps.example.com:

```
dig -t NS dnsseed.example.com
```

```
;; ANSWER SECTION
dnsseed.example.com.   86400    IN      NS     vps.example.com.

On the system vps.example.com, you can now run dnsseed:

./dnsseed -h dnsseed.example.com -n vps.example.com


If you want the DNS server to report SOA records, please provide an
e-mail address (with the @ part replaced by .) using -m.

### COMPILING
---------
Go into the seeder directory and run "make". 
```
cd sumcoin-seeder
```

Compiling will require boost and ssl.  On debian systems, these are provided
by `libboost-dev` and `libssl-dev` respectively.

From the dir - "sumcoin-seeder" run:
```
make
```
* This will produce the `dnsseed` binary.

* It should compile pretty quickly.

## Create TMUX Session

When it's done, start a tmux session called "seeder".  ** STAY in the dir "sumcoin-seeder"

```
tmux new -s seeder
```

Now enter the TMUX Session
```
tmux a -t seeder
```

Start the dnsseeder with the following:
```
./dnsseed -h dnsseed.domain.com -n vps.domain.com -m emailaddress.domainname.com --wipeignore
```



## RUNNING AS NON-ROOT


Typically, you'll need root privileges to listen to port 53 (name service).

One solution is using an iptables rule (Linux only) to redirect it to
a non-privileged port:

$ iptables -t nat -A PREROUTING -p udp --dport 53 -j REDIRECT --to-port 5353

If properly configured, this will allow you to run dnsseed in userspace, using
the -p 5353 option.
