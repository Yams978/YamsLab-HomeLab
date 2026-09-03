# Troubleshooting: Uptime Kuma Could Not Resolve Tailscale MagicDNS Names

## Overview

While configuring Uptime Kuma to monitor services across the YamsLab environment, I encountered an issue where services could be reached normally using their Tailscale MagicDNS hostnames from the host system, but Uptime Kuma could not resolve those same names from inside its Docker container.

This troubleshooting exercise helped reinforce concepts involving Docker networking, DNS resolution, host networking, and service monitoring.

---

## Environment

The affected environment included:

- Ubuntu Server
- Docker
- Uptime Kuma
- Tailscale
- Tailscale MagicDNS
- Multiple YamsLab services
- Proxmox hosts
- Jellyfin
- Homepage

---

## Symptoms

Uptime Kuma was able to run normally, but monitors using Tailscale hostnames failed.

Examples of the type of addresses being monitored included:

`http://hostname:port`

`https://hostname:port`

The same hostnames worked outside the container, which indicated that the services themselves were available.

This suggested the issue was related to name resolution or container networking rather than the monitored applications.

---

## Troubleshooting Process

### 1. Verified Service Availability

I first confirmed that the target services were running and reachable from another system.

This helped rule out:

- Application failure
- Server shutdown
- Incorrect service ports
- General network outages

### 2. Compared Host vs. Container Connectivity

The Tailscale MagicDNS hostnames resolved correctly from the Docker host.

However, Uptime Kuma was running inside its own Docker network namespace and was not resolving those names in the same way as the host.

This narrowed the problem down to Docker networking and DNS behavior.

### 3. Identified the Networking Difference

Tailscale was running on the Ubuntu host.

The host had access to the Tailscale networking and DNS configuration, while the Uptime Kuma container was using Docker's normal container networking.

As a result, the container did not have the same network/DNS behavior as the host.

---

## Resolution

Uptime Kuma was reconfigured to use Docker **host networking**.

Using host networking allowed Uptime Kuma to share the host's network stack and resolve the Tailscale MagicDNS hostnames correctly.

After the change, monitors using friendly Tailscale names began working successfully.

Examples included monitoring:

- Jellyfin
- Proxmox hosts
- Homepage
- Other internal YamsLab services

---

## Validation

After changing the networking configuration, I verified that:

- Uptime Kuma remained accessible
- Tailscale hostnames resolved correctly
- Jellyfin monitoring succeeded
- Proxmox monitoring succeeded
- Homepage monitoring succeeded
- HTTPS monitors could be configured appropriately for internal self-signed certificates

---

## Root Cause

The issue was caused by a difference between the Docker container's networking environment and the host's networking environment.

The Ubuntu host had direct access to Tailscale and MagicDNS, while the container's default Docker network did not inherit the same DNS and routing behavior.

---

## What I Learned

This issue reinforced several networking concepts:

- Containers have their own networking environment
- DNS resolution can differ between a host and a container
- Successful connectivity from the host does not guarantee identical connectivity inside Docker
- Docker host networking can be useful when a container needs access to host-level networking behavior
- Testing each layer separately helps isolate networking problems
- Monitoring tools are useful for validating infrastructure changes

---

## Skills Demonstrated

- Docker networking
- DNS troubleshooting
- Tailscale
- MagicDNS
- Linux networking
- Service monitoring
- Network troubleshooting
- Root-cause analysis
