---
title: Gamarr Appdata Directory
description: Guide to Gamarr application data directory structure, configuration files, and data management
published: true
date: 2025-02-02T00:00:00.000Z
tags: gamarr, appdata, configuration, directory, files, data, structure
editor: markdown
dateCreated: 2025-02-02T00:00:00.000Z
---

> Below are the default paths for the application data directory {.is-info}

> All instances of `$USER` are placeholders for the user the application is running under. {.is-warning}

# Windows

`C:\ProgramData\Gamarr`

# Linux

Unless otherwise specified Gamarr will store it's application data in the home folder of the user Gamarr is running under `/home/$USER/.config/Gamarr` or `~/.config/Gamarr`

The installation instructions specify `/var/lib/gamarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/Library/Application Support/Gamarr` or `~/Library/Application Support/Gamarr`

# Synology

`/usr/local/Gamarr/var/.config/Gamarr`

`/volume1/@appstore/Gamarr/var/.config/Gamarr'

'/volume1/@appdata/gamarr/.config/Gamarr'

# QNAP

`/share/MD0_DATA/homes/admin/.config/Gamarr`

`/share/CACHEDEV1_DATA/Gamarr_CONFIG`

# Docker

`/config`

- This will vary based on where the user maps `/config` to on their host system

# Arguments

The `-data=` argument forces the location of the AppData folder, so your startup command may be forcing a specific location. This is required when trying to run multiple instances. On Windows this would be `/data=`

The `-nobrowser` argument refrains from launching/opening the browser on startup. On Windows this would be `/nobrowser`
