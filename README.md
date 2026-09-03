# Campus / NCE Containerlab Lab

Portable copy of the NCE campus lab from `sphoffman/containerlab-labs`.

This repository contains the topology, current Junos startup configurations, LabHost startup scripts, and the IP-address planning notes. Containerlab runtime state, packet captures, generated inventories, backup files, historical configuration experiments, and authentication hashes are intentionally excluded.

## Prerequisites

- Containerlab
- The Juniper vrnetlab images named in `NCE.clab.yml`
- `containerlab-infrastructure` with `labmgmt` installed
- The public LabHost image:

```bash
docker pull ghcr.io/sphoffman/labhost:1.4
```

## Install into containerlab-infrastructure

From the infrastructure repository:

```bash
git clone https://github.com/sphoffman/Campus.git labs/NCE
labmgmt onboard --dry-run labs/NCE/NCE.clab.yml
labmgmt onboard labs/NCE/NCE.clab.yml
sudo containerlab deploy -t labs/NCE/NCE.clab.yml
```

The topology deliberately contains no `mgmt:` block or `mgmt-ipv4:` values. `labmgmt onboard` allocates a management subnet and stable node addresses for the new server.

## Credentials

Public startup configurations do not contain password hashes. Supply the Junos automation password locally:

```bash
export LABMGMT_JUNOS_PASSWORD='your-lab-password'
```

If the destination images do not retain their normal lab credentials when loading the sanitized configurations, set the local test-account password from the device console before using `labmgmt save`.

After cloning, make this repository private before committing any credentials, sensitive customer data, or future device configurations.
