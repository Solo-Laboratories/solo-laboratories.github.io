# k3s
Yes, I know. All of this is well documented on [their website](https://docs.k3s.io/quick-start) but this cuts the fat and jumps straight to the point with examples.

## Adding Agents to Cluster

So you have a k3s server setup but you want to add more nodes OR you realize you need more nodes and forgot/too lazy to look up how. Well, follow the steps below and we will get you where you want to be.

1. Grab the token from the server node or on that paper you wrote it on so you didn't forget.

```bash
ssh -t user@control-node-1 'cat /var/lib/rancher/k3s/server/node-token'
```
Note the username is probably not 'user' nor is your ip address/domain of the server 'control-node-1'. Use what matches your environment. For me it is 'billy@10.1.0.164'. Anyway, that will cat out your token that you will be using in the next step. OR if you're clever, combine the steps into one nasty looking one liner. I won't do that here (maybe come back in the future and do it) so I can talk about each step.

2. Use K3s wonder installer script to install K3s on your new server. I am assuming you've already stood a server running your favourite linux distro. If not, come back later when I've had time to write that part of the helping hand guide. Anyway - MAGIC TIME!

```bash
ssh -t user@new-agent-node-5 'curl -sfL https://get.k3s.io | K3S_URL=https://control-node-1-ip-or-domain:6443 K3S_TOKEN="mySpecialTokenFromStep1" sh -'
```

Again - not my work; I am just trying to give you a fun TLDR of [this quick start guide](https://docs.k3s.io/quick-start) for installing a new agent.

If you installed your previous agent nodes with special arguments, I'd suggest you run a history to figure out what you did on your previous agent node and apply the same arguments during installation here.

3. Profit! Use whatever tool you use to interface with your cluster to view the new node under the 'nodes' kind object selection.