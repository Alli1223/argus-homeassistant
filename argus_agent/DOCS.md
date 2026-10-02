# Argus Agent

Runs the [Argus](https://github.com/Alli1223/Argus) agent on your Home Assistant machine, so it shows up
in Argus next to your other systems: CPU, memory, load, disks, network, temperatures, the busiest
processes, and Home Assistant's containers.

## Setup

1. In Argus, open **Add a system** and create an enrollment token (step 1). Copy it; it
   starts with `argus_et_`. You can skip the installer step.
2. In this add-on's **Configuration** tab, fill in:
   - **Argus server URL**: the address you open Argus at, such as `https://argus.example.com`.
   - **Enrollment token**: the token from step 1.
3. Start the add-on. Within a minute the machine appears on Argus's **Hosts** page. Its name is the
   machine's hostname (usually `homeassistant`); rename it in Argus if you like.

The token is only used the first time. After that the agent keeps its own key in the add-on's data,
so you can clear the token from the configuration.

## Options

| Option | What it does |
| --- | --- |
| Argus server URL | Where the agent reports. Use `https`; with plain `http` the agent's key travels unencrypted. |
| Enrollment token | Registers the machine the first time the agent starts. |
| Allow container actions | Lets people who can see this machine in Argus read container logs and start, stop and restart containers, Home Assistant's own included. Off by default. |
| Read SATA drive temperatures | Also reads SATA drives' temperatures. On some drives this stops them spinning down. NVMe drives are always read. |

## What the add-on is allowed to do, and why

The add-on watches the whole machine, not just its own container, so it asks for more access than
most add-ons and has a low security rating:

- **Host network and host processes**: the machine's own network counters and addresses, and its
  processes rather than the container's.
- **AppArmor off and the `SYS_PTRACE` capability**: the agent reads the machine's `/proc`, `/sys` and
  `/etc` through `/proc/1/root`. That gives the right operating system name, every disk, and a machine
  ID that stays the same if the add-on is reinstalled. It only reads; nothing is written there.
- **Docker API**: lists Home Assistant's containers (Core, Supervisor and each add-on). Home Assistant
  only grants it with **Protection mode** turned off on the add-on's **Info** tab. With Protection mode
  on, everything except containers is still reported.

## Updates

The agent can't update itself here, because the add-on's version is the agent's version. When Argus
offers an agent update for this machine, update the add-on in Home Assistant instead.

## Troubleshooting

The add-on's **Log** tab shows what the agent is doing. Common messages:

- *Registration failed (Unauthorized)*: the enrollment token is wrong, expired or used up. Create a
  new one in Argus.
- *Could not send metrics*: Home Assistant can't reach the server URL. Samples are kept and sent once
  the server is reachable again.
- *Access to the path '/proc/1/root/…' is denied*: the add-on is not getting the access above. Check
  that it is the latest version, then restart it.
