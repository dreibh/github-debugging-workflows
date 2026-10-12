# GitHub Debugging Workflows

# 💡 What are the GitHub Debugging Workflows?

This repository contains GitHub Workflows for debugging GitHub Workflow instances interactively using SSH access via a [Tailscale](https://tailscale.com/) VPN:

* MacOS Debugging Workflow:
  [`.github/workflows/debug-tailscale-macos.yaml`](.github/workflows/debug-tailscale-macos.yaml)
* Ubuntu Debugging Workflow:
  [`.github/workflows/debug-tailscale-ubuntu.yaml`](.github/workflows/debug-tailscale-ubuntu.yaml)
* Windows Debugging Workflow:
  [`.github/workflows/debug-tailscale-windows.yaml`](.github/workflows/debug-tailscale-windows.yaml)


Each debugging workflow performs the following steps:

1. Installation of Tailscale and setup of a Tailscale VPN tunnel to allow SSH access to the instance.
2. Installation of build dependencies, particularly for build tests of:

  - [System-Tools](https://github.com/dreibh/system-tools/) (see [System-Tools – Tools for Basic System Management](https://www.nntb.no/~dreibh/system-tools/))
  - [Virtual Machine Image Builder and System Installation Scripts](https://github.com/simula/nornet-vmimage-builder-scripts/) (see [Virtual Machine Image Builder and System Installation Scripts](https://www.nntb.no/~dreibh/vmimage-builder-scripts/))
  - [HiPerConTracer](https://github.com/dreibh/hipercontracer/) (see [HiPerConTracer – High-Performance Connectivity Tracer](https://www.nntb.no/~dreibh/hipercontracer/))
  - [NetPerfMeter](https://github.com/dreibh/netperfmeter/) (see [NetPerfMeter – A TCP/MPTCP/UDP/SCTP/DCCP Network Performance Meter Tool](https://www.nntb.no/~dreibh/netperfmeter/))
  - [SubNetCalc](https://github.com/dreibh/subnetcalc/) (see [SubNetCalc – An IPv4/IPv6 Subnet Calculator](https://www.nntb.no/~dreibh/subnetcalc/))
  - [Dynamic Multi-Homing Setup (DynMHS)](https://www.nntb.no/~dreibh/dynmhs/)
  - [BibTeXConv](https://github.com/dreibh/bibtexconv/) (see [BibTeXConv – A BibTeX File Converter](https://www.nntb.no/~dreibh/bibtexconv/))
  - [FractGen](https://github.com/dreibh/fractgen/) (see [FractGen – An Extensible Fractal Generator](https://www.nntb.no/~dreibh/fractalgenerator/))


3. Configuration of the environment to make debugging more comfortable.


# 💻 Access to Workflow Instances via SSH

## Prepare a client machine

1. Set up a [Tailscale](https://tailscale.com/) VPN, e.g., in an Ubuntu VM or container:

  ```bash
  curl -fsSL https://tailscale.com/install.sh | sh
  sudo tailscale up
  ```

  You may need to authenticate to Tailscale with GitHub.

  It is strongly recommended to install [System-Tools](https://www.nntb.no/~dreibh/system-tools/) as well:

  ```bash
  sudo apt-add-repository -y ppa:dreibh/ppa
  sudo apt install -y td-system-tools-basic
  ```

  Run `System-Info` and check the network interfaces. It must show a Tailscale interface `tailscale0` with Tailscale IP addresses.


## Add the debugging workflows to your repository

Copy the workflow YAML files from [`.github/workflows`](.github/workflows/) of this repository to the corresponding directory of your repository:

* Ubuntu Debugging Workflow:
  [`.github/workflows/debug-tailscale-ubuntu.yaml`](.github/workflows/debug-tailscale-ubuntu.yaml)
* MacOS Debugging Workflow:
  [`.github/workflows/debug-tailscale-macos.yaml`](.github/workflows/debug-tailscale-macos.yaml)
* Windows Debugging Workflow:
  [`.github/workflows/debug-tailscale-windows.yaml`](.github/workflows/debug-tailscale-windows.yaml)

Add the files, commit, and push.

## Manually start an instance on GitHub

1. Log into [GitHub](https://www.github.com) and go to your repository.

2. Clicking on _Actions_ shows the debugging workflows, i.e.:

  * MacOS Debugging Workflow via Tailscale
  * Ubuntu Debugging Workflow via Tailscale
  * Windows Debugging Workflow via Tailscale

  Select a workflow, e.g., "MacOS Debugging Workflow via Tailscale", and start this workflow under "Run workflow".

3. Open the log of the running instance and look for the Tailscale SSH details of the instance:

  ```
  ====== 2026-10-09 07:50:35 +0000 ==========================================
  Tailscale IPs: 100.100.210.26 fd7a:115c:a1e0::892a:d21b
  Connect via SSH using:
  * ssh runner@100.100.210.26
  * ssh runner@fd7a:115c:a1e0::892a:d21b
  SSH key fingerprints:
  * #1: SHA256:hiJFRr3JzLwHMfHci6Uu3N2sH6IxndWxS21nRrbf18k (ECDSA 256)
  * #2: SHA256:W1Rh/k/tWxgJFSwvzf/E3mzaJvCIXpNtUl/e1bYMRCo (ED25519 256)
  * #3: SHA256:+g20wQO5bJyYRO4aYq/utzpc47Pi9Iavt9nUwvmdSmE (RSA 3072)
  ===========================================================================
  ```

4. Call the displayed SSH command from the client machine, e.g.:

  ```bash
  ssh runner@100.100.210.26
  ```

  The log also contains the SSH server's key fingerprints, for verifying the key fingerprint presented by the client before accepting a new key.

  You may need to authenticate to Tailscale with GitHub.

  For Windows instances, connect using `runneradmin` (e.g., `ssh runneradmin@100.100.210.26`) and authenticate using either the displayed password or your GitHub SSH key.


# 🔗 Useful Links

## System Management Software

* [System-Tools – Tools for Basic System Management](https://www.nntb.no/~dreibh/system-tools/)
* [Build-Tools – Tools for Software Packaging](https://www.nntb.no/~dreibh/build-tools/)
* [Virtual Machine Image Builder and System Installation Scripts](https://www.nntb.no/~dreibh/vmimage-builder-scripts/)

## Networking Software

* [NetPerfMeter – A TCP/MPTCP/UDP/SCTP/DCCP Network Performance Meter Tool](https://www.nntb.no/~dreibh/netperfmeter/)
* [HiPerConTracer – High-Performance Connectivity Tracer](https://www.nntb.no/~dreibh/hipercontracer/)
* [SubNetCalc – An IPv4/IPv6 Subnet Calculator](https://www.nntb.no/~dreibh/subnetcalc/)
* [Dynamic Multi-Homing Setup (DynMHS)](https://www.nntb.no/~dreibh/dynmhs/)
