<p align="center">
  <img src="mascot.webp" width="300" alt="Mel, the SwarmSync mascot: a bee boy with antennae in a black-and-yellow hoodie, in front of a honeycomb, syncing an upload folder and a download folder"><br>
  <i>Mel the SwarmSync mascot</i>
</p>

<h1 align="center">SwarmSync</h1>

<p align="center"><b>Pair once. Sync everywhere.</b></p>

<h3 align="center">Coming soon</h3>

Peer-to-peer file sync for your own Linux machines. Each one becomes a bee in your swarm: pair them once, pick the folders, and the bees keep them in sync directly with each other. No cloud in the middle.

**Think Syncthing, but simpler.**

- **Pair once.** Add a new machine through any bee, and the whole swarm trusts it. No adding devices on every machine.
- **Pick, don't configure.** Share whole folders or single files, from your home all the way up to `/`. Every bee sees every share; subscribe with one command, at the same path or your own.
- **Bee to bee, encrypted.** Files travel directly between your machines over QUIC and TLS 1.3. No cloud stores them, and the small resolver that helps bees find each other never sees them.
- **Made for switching machines.** Laptop, home PC, work PC: changes go out about a second after you save, and a closing lid waits until they're sent.
- **Permissions included.** File modes travel with the files, so even config files in `/etc` arrive the way they left.
- **Light and Linux-native.** One small daemon and a simple command-line tool, from servers down to a Raspberry Pi.

## Example: one .vimrc on two machines

*Planned commands; file syncing is being built.*

```
# alpha: create the swarm. It gets six words; bees are named after their hostname.
alpha$ swarmsync init
swarm created: water swing forest jelly mutual hint
alpha$ swarmsync invite
pairing open for 10 minutes. This bee: alpha  BLAKE3:Wq7f…3kZ
waiting for a bee...

# beta, anywhere, behind NAT or not: join with the six words.
# First contact: is this alpha's key? Compare it with alpha's screen.
beta$ swarmsync join water swing forest jelly mutual hint
Bee:         alpha
Fingerprint: BLAKE3:Wq7f…3kZ
Trust this bee and ask to join? [y/N] y

# alpha, still waiting: is this beta's key? beta shows it with `swarmsync id`.
beta wants to join, from 192.0.2.20.
Fingerprint: BLAKE3:p2Lx…9Qe
Accept? [y/N] y
beta joined the swarm

# alpha: share the file
alpha$ swarmsync add /home/user/.vimrc

# beta: subscribe, same path
beta$ swarmsync sync .vimrc@alpha --same
```

**No addresses needed.** The six words find your swarm through a small resolver, wherever your machines are and whatever their IP addresses are today. They only work while one of your bees runs `invite`; the swarm's real ID is a random UUID.

**Trust on first use.** The first time two bees meet, each shows the other's key fingerprint (shortened above), and you compare it once with what the other machine shows. From then on the key is the bee's identity: every bee in the swarm knows it, a machine with any other key is turned away, and there are no accounts, passwords or certificates. A third machine pairs with any one bee and is then trusted by all of them.

Now edit `.vimrc` on either machine, and about a second later the other one has it.

Website: [swarmsync.net](https://swarmsync.net)
