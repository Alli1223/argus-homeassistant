# Argus for Home Assistant

A Home Assistant add-on that runs the [Argus](https://github.com/Alli1223/Argus) agent, so your Home
Assistant machine reports to Argus like any other system.

It needs Home Assistant OS or a Supervised install, on a 64-bit machine (`amd64` or `aarch64`, such as
a Raspberry Pi 4 or 5 running the 64-bit image).

## Install

[![Add repository to Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2FAlli1223%2Fargus-homeassistant)

Or in Home Assistant: **Settings → Add-ons → Add-on store**, then **⋮ → Repositories**, and add
`https://github.com/Alli1223/argus-homeassistant`.

Then install **Argus Agent** and follow its Documentation tab.

## Versions

The add-on runs the agent image Argus publishes (`ghcr.io/alli1223/argus-agent`), and its version is
the Argus release it runs. Each Argus release gets an add-on release with the same version.
