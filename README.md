<div align="center">

### <img src="res/k8s-logo.png" align="center" width="30px" height="30px"/> Homelab <img src="res/k3s-logo.png" align="center" width="30px" height="30px"/>

_Automatically managed with Flux, Renovate, and Github Actions_ 🤖

</div>


<div align="center">

![Dynamic YAML Badge](https://img.shields.io/badge/dynamic/yaml?url=https%3A%2F%2Fraw.githubusercontent.com%2Fhomelab-peej%2Fk8s-at-home%2Frefs%2Fheads%2Fmain%2Fkubernetes%2Fapps%2Fsystem-upgrade-controller%2Fapp%2Fplan-server.yaml&query=%24.spec.version&style=flat&label=Kubernetes)
  ![Flux](https://badgen.net/badge/Flux/2.5.1/blue) [![yamllint](https://github.com/homelab-peej/k8s-at-home/actions/workflows/yamllint.yaml/badge.svg?branch=main&event=push)](https://github.com/homelab-peej/k8s-at-home/actions/workflows/yamllint.yaml)

</div>

## 🛠️ Tools

| Tool                                     | Purpose                                                                          |
|------------------------------------------|----------------------------------------------------------------------------------|
| [Flux](https://fluxcd.io/flux/)          | Operator to manage your K8S cluster based any number of sources including GitHub |
| [Renovate](https://docs.renovatebot.com) | Tool to automate dependency updates                                              |
| [SOPS](https://github.com/getsops/sops)  | K8S secrets and configmap manager to encrypt secrets with GnuPG for storage      |


## 🖥️ Nodes

| Node            | RAM  | Storage                   | Role   | OS            | Accessories                                                                            |
|-----------------|------|---------------------------|--------|---------------|----------------------------------------------------------------------------------------|
| Raspberry Pi 5  | 8GB  | 256GB NVMe SSD            | Master | Raspbian Lite | [Hat](https://www.waveshare.com/poe-m.2-hat-plus.htm), [Drive](https://a.co/d/4kcOG6z) |
| Raspberry Pi 5  | 8GB  | 256GB NVMe SSD            | Master | Raspbian Lite | [Hat](https://www.waveshare.com/poe-m.2-hat-plus.htm), [Drive](https://a.co/d/4kcOG6z) |
| Raspberry Pi 5  | 8GB  | 256GB NVMe SSD            | Master | Raspbian Lite | [Hat](https://www.waveshare.com/poe-m.2-hat-plus.htm), [Drive](https://a.co/d/4kcOG6z) |
| Raspberry Pi 5  | 8GB  | 256GB NVMe SSD            | Worker | Raspbian Lite | [Hat](https://www.waveshare.com/poe-m.2-hat-plus.htm), [Drive](https://a.co/d/4kcOG6z) |
| Raspberry Pi 5  | 8GB  | 256GB NVMe SSD            | Worker | Raspbian Lite | [Hat](https://www.waveshare.com/poe-m.2-hat-plus.htm), [Drive](https://a.co/d/4kcOG6z) |
| N95 Mini PC     | 32GB | 2TB NVMe SSD              | Worker | Debian        |                                                                                        |


## 📦 Storage

| Node    | RAM   | Storage             | Function              | OS            |
|---------|-------|---------------------|-----------------------|---------------|
| TrueNAS | 128GB | 12 x 8TB HDD RAIDZ3 | Multi-purpose Storage | TrueNAS Scale |


## 🛜 Network 

| Vendor   | Model             | Function                                        |
|----------|-------------------|-------------------------------------------------|
| Ubiquiti | Dream Machine Pro | Primary Router, Camera Storage, Network Manager |
| Ubiquiti | US-48-500W        | Rack switch with PoE and 10G SFP+               |
| Ubiquiti | U6-LR             | Wireless Access Point                           |


## ☁️ Cloud Services

| Service                                              | Use                                        | Cost            |
|------------------------------------------------------|--------------------------------------------|-----------------|
| [Backblaze](https://www.backblaze.com/cloud-storage) | Offsite S3 storage for important files     | ~$100/yr        |
| [Bitwarden](https://bitwarden.com)                   | Password management                        | Free            |
| [Cloudflare](https://www.cloudflare.com/)            | Domains and DNS management                 | ~$70/yr         |
| [GitHub](https://github.com/)                        | Hosting this repo and CI/CD                | Free            |
| [Let's Encrypt](https://letsencrypt.org/)            | Issuing SSL Certificates with Cert Manager | Free            |
| [UniFi Site Manager](https://unifi.ui.com)           | UniFi External Access Management           | Free            |
|                                                      |                                            | Total: ~$170/yr |
