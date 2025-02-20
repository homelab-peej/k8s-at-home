<div align="center">

### Homelab ⚗️ 

_Automatically managed with Flux and Github Actions_ 🤖

</div>


<div align="center">

![Kubernetes](https://badgen.net/badge/Kubernetes/1.31.5+k3s1/blue)  ![Flux](https://badgen.net/badge/Flux/2.5.0/blue) [![yamllint](https://github.com/homelab-peej/k8s-at-home/actions/workflows/yamllint.yaml/badge.svg?branch=main&event=push)](https://github.com/homelab-peej/k8s-at-home/actions/workflows/yamllint.yaml)

</div>

## 🛠️ Tools

| Tool                            | Purpose                                                                          |
|---------------------------------|----------------------------------------------------------------------------------|
| [Flux](https://fluxcd.io/flux/) | Operator to manage your K8S cluster based any number of sources including GitHub |


## 🖥️ Nodes 
| Node           | RAM | Storage        | Role   | OS            |
|----------------|-----|----------------|--------|---------------|
| Raspberry Pi 5 | 8GB | 256GB NVMe SSD | Master | Raspbian Lite |
| Raspberry Pi 5 | 8GB | 256GB NVMe SSD | Worker | Raspbian Lite |
| Raspberry Pi 5 | 8GB | 256GB NVMe SSD | Worker | Raspbian Lite |
| Raspberry Pi 5 | 8GB | 256GB NVMe SSD | Worker | Raspbian Lite |


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

| Service                                              | Use                                    | Cost            |
|------------------------------------------------------|----------------------------------------|-----------------|
| [Cloudflare](https://www.cloudflare.com/)            | Domains and DNS management             | ~$70/yr         |
| [Backblaze](https://www.backblaze.com/cloud-storage) | Offsite S3 storage for important files | ~$100/yr        |
| [GitHub](https://github.com/)                        | Hosting this repo and CI/CD            | Free            |
|                                                      |                                        | Total: ~$170/yr |
