<p align="center">
  <img src="mascot.webp" width="300" alt="Mel, the SwarmSync mascot: a bee boy with antennae in a black-and-yellow hoodie, in front of a honeycomb, syncing an upload folder and a download folder"><br>
  <i>Mel the SwarmSync mascot</i>
</p>

<h1 align="center">SwarmSync</h1>

<p align="center"><b>Pair once. Sync everywhere.</b></p>

<h3 align="center">Coming soon</h3>

Peer-to-peer file sync for your own machines, Linux first, with an Android app planned. Each one becomes a bee in your swarm: pair them once, pick the folders, and the bees keep them in sync directly with each other. No cloud in the middle.

**Think Syncthing, but simpler.**

- **Pair once.** Add a new machine through any bee, and the whole swarm trusts it. No adding devices on every machine.
- **No limit in sight.** Start with two machines and keep adding bees: swarms are built to grow practically without limit.
- **Pick, don't configure.** Share whole folders or single files, from your home all the way up to `/`. Every bee sees every share; subscribe with one command, at the same path or your own.
- **Bee to bee, wherever they are.** Files travel directly between your machines, encrypted with QUIC and TLS 1.3: on the same network, through NAT or over Tailscale, and through one of your other bees when there's no direct way. No cloud stores them, and the small resolver that helps bees find each other never sees them.
- **Made for switching machines.** Laptop, home PC, work PC: changes go out about a second after you save, and a closing lid waits until they're sent.
- **Permissions included.** File modes travel with the files, so even config files in `/etc` arrive the way they left.
- **Nothing lost by accident.** If two machines changed the same file, the newer version wins and the other is kept aside, one command away. A drive that isn't plugged in pauses its share instead of deleting your files everywhere.
- **Light, Linux first.** One small daemon and a simple command-line tool, from servers down to a Raspberry Pi. An Android app is planned.

## Example: one .vimrc on two machines

*Syncing already works between test machines; the first release is still to come.*

```
# alpha: start a swarm and open pairing
alpha$ swarmsync init
swarm created: water swing forest jelly mutual hint
this bee: alpha  BLAKE3:Wq7f…3kZ
alpha$ swarmsync invite
pairing open for 10 minutes. This bee: alpha  BLAKE3:Wq7f…3kZ
on the new bee: swarmsync join water swing forest jelly mutual hint
waiting for a bee...

# beta: join with the six words
beta$ swarmsync join water swing forest jelly mutual hint
Bee:         alpha
Fingerprint: BLAKE3:Wq7f…3kZ
Trust this bee and ask to join? [y/N] y
waiting for the other bee to accept...

# alpha, still in invite
beta wants to join, from 192.0.2.20.
Fingerprint: BLAKE3:p2Lx…9Qe
Accept? [y/N] y
beta joined the swarm

# beta
joined swarm water swing forest jelly mutual hint as beta

# share the file on alpha, pick it up on beta
alpha$ swarmsync add ~/.vimrc
published .vimrc@alpha (file ~/.vimrc)
other bees subscribe with: swarmsync sync .vimrc@alpha --same
beta$ swarmsync sync .vimrc@alpha --same
subscribed to .vimrc@alpha at /home/user/.vimrc
```

That's it: edit `.vimrc` on either machine, and about a second later the other one has it.

**No addresses, no accounts.** The six words find your swarm wherever your machines are. While pairing, each machine shows the other's key fingerprint once (shortened above); you compare it with what the other machine shows and type `y`. From then on that key is the bee's identity, trusted by every bee in the swarm. A third machine pairs with any one bee the same way.

Website: [swarmsync.net](https://swarmsync.net)
