# THIS REPO IS AN EXPERIMENT, don't commit here.

The following is how I made all these experiment directories, each of which contains the `spoilers.json` chopped into pieces small enough to edit using the github web interface.

Note that this results in invalid JSON because the splits occur in the middle of objects.

    $ cat spoilers.json |aeson-pretty > spoilers2.json && mv spoilers2.json spoilers.json
    $ for i in `seq 2 10`; do mkdir split-experiment.$i; cd split-experiment.$i; split -e --verbose \
      --additional-suffix=.json -n $i ../spoilers.json spoilers.; cd ..; done

## Results

Split four ways is still too big.  Split five ways works, but editor performance is poor because the file is so big.  I say you go for split 10 ways.

# original README follows...

# Beware! Spoilers ahead!

Spoilerwall introduces a brand new concept in the field of network hardening. Avoid being scanned by spoiling movies on all your ports!

Firewall? How about Fire'em'all! Stop spending thousand of dollars on big teams that you don't need! Just fire up the Spoilers Server and that's it!

Movie Spoilers DB + Open Ports + Pure Evil = Spoilerwall

Set your own:

1. Clone this repo

```
$ git clone git@github.com:infobyte/spoilerwall.git
```

2. Edit the file `server-spoiler.py` and set the **HOST** and **PORT** variables.

3. Change spoiler color (or not?), default green

4. Run the server

```
$ python2 server-spoiler.py
```

The server will listen on the selected port (8080 by default). Redirect incoming TCP traffic in all ports to this service by running:

```
iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 1:65535 -j DNAT --to-destination {HOST}:{PORT}
```

Change **{HOST}** and **{PORT}** for the values set in step (2). Also, if the traffic is redirected to localhost, run:

```
sysctl -w net.ipv4.conf.eth0.route_localnet=1
```

Using this config, an nmap scan will show every port as open and a spoiler for each one.

View the live demo running in [spoilerwall.faradaysec.com](http://spoilerwall.faradaysec.com)

```
~ ❯❯❯ telnet spoilerwall.faradaysec.com 23

Trying 138.197.196.144...

Connected to spoilerwall.faradaysec.com.

Escape character is '^]'.

Gummo

Fucked up people killing cats after a tornado

Connection closed by foreign host.
```

Browse in Shodan (but beware of the Spoilers!):

https://www.shodan.io/host/138.197.196.144

Be careful in your next CTF - you never know when the spoilers are coming!

Spoilers from **SpoilMe**: https://spoilme.io 
Thanks **SpoilMe**!
