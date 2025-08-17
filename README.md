# linux-net-playground
## Introduction
> This is a home project, done to understand Linux, networking and security better. **This is not a manual for a production environment setup!**
> Work is in continuous progress, and nothing is finalized yet. **Use at your own risk!**
>
> Everything is provided **"as is"** for educational and research purposese, the author makes **no warranties** and assumes **no responsibility or liability** for any issues, damage or consequences resulting from the use of anything stored in this repository!

The structure currently in use is the following:
```text
- repo-root/
  - README.md
  - .gitignore
  - temporary/      # temporary files, notes, drafts
  - baseline/       # initial VM + network setup
  - lab_001/        # first lab
  - ...
  - lab_x/          # following labs
```
## Scope
Scope includes the topics: Local VM (Virtual Machine), Containers, Linux Desktop, Linux Server, Networking, Routing, Firewall, SIEM, Vulnerability Scanner, etc.. 

Particualr OSs (Operating Systems), platforms, tools, virtualization software used:
- VirtualBox
- Docker
- OPNsense
- Ubuntu Server
- OpenSuse Leap
- Wazuh
- Lynis
- Oscap
- ...
## Hardware recommendations
Hardware recommendations: powerfull multi-core CPU that supports virtualization, 32 GB RAM (you can try with 16 GB as well, depending on the host OS it might be enough to launch the baseline at least), fast 1 TB SSD (better if it is a dedicated "internal" SSD, not a USB connected "external" one).
