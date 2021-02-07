# Overline relay node

This runs an Overline node in relay-only mode (not mining).

## Should I bother to read this README.md?

You should.

## What's required

- Docker
- docker-compose
- 10G RAM (it may work with less but may crash every now and then)

## Why would you want to run a relay-only Overline node?

1. To use it as your private Interchange backend
2. To help the network
3. Both

## How to run it

First, create a file named ```.env``` and store your secure cookie as a key-value pair in it. Something like ```SCOOKIE=mysecretstring```

Now, unless you're using Traefik in front of your Docker stuff you need to uncomment the line in ```docker-compose.yml``` that starts with 'uncomment this if you're not using Traefik'. 
If you don't uncomment this line, you won't be able to connect to your relay in an unsecure way.

If you want to sync from the Genesis block, you just ```docker-compose up -d```

If you want to use an existing blockchain dump to speed up the inital sync, see below.

## My relay-node is syncing old blocks forever

Download a recent blockchain dump and import it into your relay node.

```
wget https://community.multichains.org/_easysync_db.zip
import-dump.sh ./_easysync_db.zip
```

Once the dump is imported, start the relay using ```docker-compse up -d```

## How can I see what the relay is doing?

```docker-compose logs -f ol-relay --tail=1000```

Or you could connect to the relay's UI which is exposed on port 9090 (if you followed the instructions above).

## How can I stop the relay node?

```docker-compose down```

## How can I stop the relay node and get rid of all blockchain data?

```docker-compose down -v```

## What's the traefik label stuff

Just ignore or remove if you're not running Traefik.
