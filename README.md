## Arch Linux System Upgrade Controller (SUC)

Upgrade [Arch Linux](https://archlinux.org) RKE2/K3s nodes with Rancher [System Upgrade Controller](https://github.com/rancher/system-upgrade-controller) (SUC).

## Why

Arch Linux is a rolling-upgrade distribution that requires frequent updates to stay secure and stable. Manually logging into multiple nodes to perform system upgrades and reboots is tedious and error-prone.

This project leverages the Rancher [System Upgrade Controller](https://github.com/rancher/system-upgrade-controller) (SUC) combined with CronJob to provide a automated system upgrade workflow.

**NOTE: Automating system upgrades and reboots carries inherent risks. Use this tool at your own risk. The maintainers are not responsible for any data loss or cluster downtime.**

## Usage

```bash
git clone https://github.com/STARRY-S/archlinux-suc && cd archlinux-suc

# Review and adjust the CronJob schedule and the upgrade script
vim archlinux-suc.yaml

# Label the target nodes for automated upgrades
kubectl label nodes "${NODE_NAME}" archlinux-os-upgrade=true

# Apply YAML config
# IMPORTANT: The first apply will immediately trigger a system update and reboot for labeled nodes
kubectl apply -f archlinux-suc.yaml

# Check upgrade pods and logs
kubectl -n cattle-system get pods

kubectl -n cattle-system logs -f apply-archlinux-system-upgrade-....
```

## License

MIT License

Copyright (c) 2026 STARRY-S

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
