---
title: Gamarr Quick Start Guide
description: Step-by-step guide to setting up and configuring Gamarr for game management
published: true
date: 2025-02-02T00:00:00.000Z
tags: gamarr, quick-start, setup, configuration, guide, installation, games
editor: markdown
dateCreated: 2025-02-02T00:00:00.000Z
---

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Quick Start Setup Guide](#quick-start-setup-guide)
- [Startup](#startup)
- [Media Management](#media-management)
  - [Game Naming](#game-naming)
  - [Importing](#importing)
  - [File Management](#file-management)
  - [Root Folders](#root-folders)
- [Profiles](#profiles)
- [Quality](#quality)
- [Indexers](#indexers)
- [Download Clients](#download-clients)
- [How to import your existing organized media library](#how-to-import-your-existing-organized-media-library)
  - [Import games](#import-games)
  - [How to add a game](#how-to-add-a-game)

# Quick Start Setup Guide

> This page is still in progress and not complete. Contributions are welcome

> For a more detailed breakdown of all the settings, check [Gamarr => Settings](/gamarr/settings)
{.is-info}

In this guide we will try to explain the basic setup you need to do to get started with Gamarr. We're going to skip some options that you may see on the screen. If you want to dive deeper into those, please see the appropriate page in the FAQ and docs for a full explanation.

> Please note that within the screenshots and GUI settings in `orange` are advanced options, so you will need to click `Show Advanced` at the top of the page to make them visible.
{.is-warning}

# Startup

After installation and starting up, you open a browser and go to `http://{your_ip_here}:6969`

# Media Management

First we're going to take a look at the `Media Management` settings where we can setup our preferred naming and file management settings.

`Settings` => `Media Management`

## Game Naming

1. Enable/Disable Renaming of your games (as opposed to leaving the names that are currently there or as they were when you downloaded them).
1. If you want illegal characters replaced or removed (`\ / : * ? " < > | ~ # % & + { }`).
1. Here you will select the naming convention for the actual game files.
1. *(Advanced Option) This is where you will set the naming convention for the folder that contains the game files.*

## Importing

1. *(Advanced Option) Enable `Use Hard links instead of Copy` more info how and why with examples [TRaSH's Hard links Guide](https://trash-guides.info/hardlinks).*
1. *(Advanced Option) Import matching extra files (nfo, etc) after importing a file.*

## File Management

1. Games deleted from disk are automatically unmonitored in Gamarr.
    - You may want to delete a game but do not want Gamarr to re-download the game. You would use this option.
1. *(Advanced Option) Designate a location for deleted files to go to (just in case you want to retrieve them before the bin is taken out).*
1. *(Advanced Option) This is how old a given file can be before it is deleted permanently.*

## Root Folders

Here we will add the root folder that Gamarr will be using to import your existing organized games library and where Gamarr will be importing (copy/hardlink/move) your games after your download client has downloaded them.

> \* Non-Windows: If you're using an NFS mount ensure `nolock` is enabled.
> \* If you're using an SMB mount ensure `nobrl` is enabled.
{.is-warning}

> **The user and group you configured Gamarr to run as must have read & write access to this location.** {.is-info}

# Profiles

`Settings` => `Profiles`

Quality Profile settings allow you to define quality tiers for your games. You can create multiple profiles for different use cases (e.g., one for games you want in the best quality, one for smaller games).

# Quality

`Settings` => `Quality`

Here you can edit quality definitions including file size limits for each quality tier.

# Indexers

`Settings` => `Indexers`

Here you'll be setting up the indexers/trackers that you'll be using to actually download any of your files.

> For more information on indexers, see [Settings => Indexers](/gamarr/settings#indexers)
{.is-info}

Once you've clicked the <kb>+</kb> button to add a new indexer you'll be presented with a new window with many different options. For the purposes of this wiki Gamarr considers both Usenet Indexers and Torrent Trackers as "Indexers".

There are two sections here: Usenet and Torrents. Based upon what download client you'll be using you'll want to select the type of indexer you'll be going with.

# Download Clients

`Settings` => `Download Clients`

Downloading and importing is where most people experience issues. From a high level perspective, the software needs to be able to communicate with your download client and have access to the files it downloads. There is a large variety of supported download clients and an even bigger variety of setups. This means that while there are some common setups, there isn't one right setup and everyone's setup can be a little different.

> See the [settings page](/gamarr/settings#download-clients), at the [More Info (Supported)](/gamarr/supported#download-clients) page for this section, and [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for more information.
{.is-info}

## Usenet

- Gamarr will send a download request to your client, and associate it with a label or category name that you have configured in the download client settings.
- Gamarr will monitor your download clients active downloads that use that category name. It monitors this via your download client's API.
- When the download is completed, Gamarr will know the final file location as reported by your download client. This file location can be almost anywhere, as long as it is somewhere separate from your games folder and accessible by Gamarr.
- Gamarr will scan that completed file location for files that Gamarr can use. It will parse the file name to match it against the requested game. If it can do that, it will rename the file according to your specifications, and move it to the specified library location.
- Atomic Moves (instant moves) are enabled by default. The file system and mounts must be the same for your completed download directory and your media library. If the atomic move fails or your setup does not support hard links and atomic moves then Gamarr will fall back and copy the file then delete from the source which is IO intensive.
- If the "Completed Download Handling - Remove" option is enabled in Gamarr's settings leftover files from the download will be sent to your trash or recycling via a request to your client to delete/remove the release.

## BitTorrent

- Gamarr will send a download request to your client, and associate it with a label or category name that you have configured in the download client settings.
- Gamarr will monitor your download clients active downloads that use that category name. This monitoring occurs via your download client's API.
- Completed downloads that are still seeding will have files left in their original location to allow you to seed the file. When downloads are removed from Gamarr, the associated files will be deleted.
- Atomic Moves (instant moves) are enabled by default. The file system and mounts must be the same for your completed download directory and your media library. If the atomic move fails or your setup does not support hard links and atomic moves then Gamarr will fall back and copy the file then delete from the source which is IO intensive.
- If the "Completed Download Handling - Remove" option is enabled in Gamarr's settings, Gamarr will delete the torrent from your client, and will ask the client to remove the torrent data, but only if the client reports that seeding is complete and torrent is stopped (paused on completion).

# How to import your existing organized media library

## Import games

Library Import allows you to import existing organized games via existing files in the path directory. This is especially useful when making a new Gamarr instance and wanting to keep your existing games.

- Navigate to Library Import
- Click the + symbol
- Select your root games folder
- Click Start Import

## How to add a game

After you've imported your existing, properly organized, media library, it's time to add the games you want.

`Library` => `Add New`

- Type the name of the game you want to add.
- Gamarr will search and return results from its metadata sources (Steam, IGDB, RAWG).
- Select the game you want to add.
- Configure the settings (Root Folder, Quality Profile, etc.)
- Click Add Game
