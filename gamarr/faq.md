---
title: Gamarr FAQ
description: Gamarr FAQ
published: true
date: 2025-02-02T00:00:00.000Z
tags: gamarr, troubleshooting, faq
editor: markdown
dateCreated: 2025-02-02T00:00:00.000Z
---

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Gamarr Basics](#gamarr-basics)
  - [How does Gamarr work?](#how-does-gamarr-work)
  - [How does Gamarr find games?](#how-does-gamarr-find-games)
  - [How do I access Gamarr from another computer?](#how-do-i-access-gamarr-from-another-computer)
  - [Forced Authentication](#forced-authentication)
  - [How are possible downloads compared?](#how-are-possible-downloads-compared)
  - [What are Lists and what can they do for me?](#what-are-lists-and-what-can-they-do-for-me)
  - [How do I update Gamarr?](#how-do-i-update-gamarr)
  - [How do I Backup/Restore Gamarr?](#how-do-i-backuprestore-gamarr)
- [Gamarr Common Problems](#gamarr-common-problems)
  - [How can I rename my game folders?](#how-can-i-rename-my-game-folders)
  - [How do I request a feature for Gamarr?](#how-do-i-request-a-feature-for-gamarr)
  - [I am getting an error: Database disk image is malformed](#i-am-getting-an-error-database-disk-image-is-malformed)
  - [Why can Gamarr not see my files on a remote server?](#why-can-gamarr-not-see-my-files-on-a-remote-server)
  - [Help I have locked myself out](#help-i-have-locked-myself-out)
  - [Weird UI Issues](#weird-ui-issues)
  - [VPNs, Jackett, and the \*ARRs](#vpns-jackett-and-the-arrs)

# Gamarr Basics

## How does Gamarr work?

- Gamarr does *not* regularly search for game files that are missing or have not met their quality goals. Instead, it fairly frequently queries your indexers and trackers for *all* the newly posted games, then compares that with its list of games that are missing or need to be upgraded. Any matches are downloaded. This lets Gamarr cover a library of *any size* with just 24-100 queries per day (RSS interval of 15-60 minutes). If you understand this, you will realize that it only covers the *future* though.
- So how do you deal with the present and past? When you're adding a game, you will need to set the correct path, profile and monitoring status then use the Start search for missing game checkbox. If the game hasn't been released yet, you do not need to initiate a search.
- Put another way, Gamarr will only find games that are newly uploaded to your indexers. It will not actively try to find games you want that were uploaded in the past.
- If you've already added the game, but now you want to search for it, you have a few choices. You can go to the game's page and use the search button, which will do a search and then automatically pick one. You can use the Search tab and see *all* the results, hand picking the one you want. Or you can use the filters of `Missing`, `Wanted`, or `Cut-off Unmet`.

## How does Gamarr find games?

> This FAQ item is a legacy FAQ Entry. Refer to [How does Gamarr work?](#how-does-gamarr-work)
{.is-info}

## How do I access Gamarr from another computer?

- By default Gamarr doesn't listen for requests from all systems (when not run as administrator), it will only listen on localhost, this is due to how the Web Server Gamarr uses integrates with Windows (this also applies for current alternatives). If Gamarr is run as an administrator it will correctly register itself with Windows as well as open the Firewall port so it can be accessed from other systems on your network. Running as admin only needs to happen once (if you change the port it will need to be re-run).

## Forced Authentication

If Gamarr is exposed so that the UI can be accessed from outside your local network then you should have some form of authentication method enabled in order to access the UI. This is also increasingly required by Trackers and Indexers.

As of Gamarr, Authentication is Mandatory.

### Authentication Method

- `Basic` (Browser pop-up) - This option when accessing your Gamarr will show a small pop-up allowing you to input a Username and Password
- `Forms` (Login Page) - This option will have a familiar looking login screen much like other websites have to allow you to log onto your Gamarr
- `External` - Configurable via Config File Only
  - If you use an **external authentication** such as Authelia, Authetik, NGINX Basic auth, etc. you can prevent needing to double authenticate by shutting down the app, setting `<AuthenticationMethod>External</AuthenticationMethod>` in the [config file](/gamarr/appdata-directory), and restarting the app. **Note that multiple `AuthenticationMethod` entries in the file is not supported and only the topmost value will be used**

### Authentication Required

- If you do not expose the app externally and/or do not wish to have auth required for local (e.g. LAN) access, then change in Settings => General Security => Authentication Required to `Disabled For Local Addresses`
  - The config file equivalent of this is `<AuthenticationRequired>DisabledForLocalAddresses</AuthenticationRequired>`

## How are possible downloads compared?

> Generally Quality Trumps All. If you wish to have Quality not be the main priority - you can merge your qualities together. [See TRaSH's Guide](https://trash-guides.info)
{.is-warning}

- The current logic [can be found here](https://github.com/gamarr-app/Gamarr/blob/main/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- As of 2025-02-02 the logic is as follows:

1. Quality
1. Custom Format Score
1. Protocol (as configured in the relevant Delay Profile)
1. Indexer Priority
1. Seeds/Peers (If Torrent)
1. Age (If Usenet)
1. Size

## What are Lists and what can they do for me?

- Lists in Gamarr allow you to import games from external sources automatically.
- Let's say you want to follow Steam recommendations or add games from a particular curator. You can create a list in Gamarr that syncs periodically.

### Why are lists sync times so long and can I change it?

- Lists are designed to be "add it and forget it" features. They sync periodically (default every 24 hours).

## How do I update Gamarr?

- Go to System and then the Updates tab to see what version of Gamarr you have and what version is available.
- To update just download and install the latest version. On Docker just pull the latest image.

### Can I update Gamarr inside my Docker container?

- *Technically* yes, but you **absolutely should not**. It's a cardinal philosophy of Docker. Database issues can arise if you upgrade your installation to the most recent `nightly`, but then update the Docker container itself (possibly downgrading to an older version).

## How do I Backup/Restore Gamarr?

### Backing up Gamarr

#### Using built-in backup

- Go to System => Backup in the Gamarr UI
- Click the Backup button
- Download the zip after the backup is created for safekeeping

#### Using file system directly

- Find the location of the AppData directory for Gamarr
  - Via the Gamarr UI go to System => About
  - [Gamarr Appdata Directory](/gamarr/appdata-directory)
- Stop Gamarr - This will prevent the database from being corrupted
- Copy the contents to a safe location

### Restoring from Backup

> Restoring to an OS that uses different paths won't work (Windows to Linux, Linux to Windows, Windows to OS X or OS X to Windows), moving between OS X and Linux may work, since both use paths containing `/` instead of `\` that Windows uses, but is not supported. You'll need to manually edit all paths in the database.
{.is-warning}

#### Using zip backup

- Re-install Gamarr (if applicable / not already installed)
- Run Gamarr
- Navigate to System => Backup
- Select Restore Backup
- Select Choose File
- Select your backup zip file
- Select Restore

# Gamarr Common Problems

## How can I rename my game folders?

- Library
- Mass Editor
- Select what games need their folder renamed
- Change Root Folder to the same Root Folder that the games currently exist in
- Select "Yes move files"

## How do I request a feature for Gamarr?

- This is an easy one [click here](https://github.com/gamarr-app/Gamarr/issues)

## I am getting an error: Database disk image is malformed

- **Errors of `Error creating log database` indicate issues with logs.db**
  - This can quickly be resolved by renaming or removing the database. The logs database contains unimportant information regarding commands history and update install history, and Info, Warn, and Error entries
- **Errors of `Error creating main database` or generic `database disk image is malformed` with no specified database indicate issues with gamarr.db**
  - Continue with the steps noted below
- This means your SQLite database that stores most of the information for Gamarr is corrupt. Your options are to try (a) backup(s), try recovering the existing database, try recovering the backup(s), or if all else fails starting over with a fresh new database.
- This error may show if the database file is not writable by the user/group \*Arr is running as. Permissions being the cause will likely only be an issue for new installs, migrated installs to a new server, if you recently modified your appdata directory permissions, or if you changed the user and group \*Arr run as.

## Why can Gamarr not see my files on a remote server?

- For all OSes ensure the user/group you're running \*Arr as has read and write access to the mounted drive.
- For Linux ensure:
  - If you're using an NFS mount ensure `nolock` is enabled.
  - If you're using an SMB mount ensure `nobrl` is enabled.
- For Windows: In short: the user \*Arr is running as (if service) or under (if tray app) cannot access the file path on the remote server. This can be for various reasons, but the most common is \*Arr is running as a service, which causes the issues described below.

### Gamarr runs under the LocalService account by default which doesn't have access to protected remote file shares

- Run Gamarr's service as another user that has access to that share
- Open the Administrative Tools \> Services window on your Windows server.
- Stop the Gamarr service.
- Open the Properties \> Log On dialog.
- Change the service user account to the target user account.

### You're using a mapped network drive (not a UNC path)

- Change your paths to UNC paths (`\\server\share`)
- Run Gamarr.exe via the Startup Folder

## Help I have locked myself out

To disable authentication (to reset your forgotten username or password) you will need need to edit `config.xml` which will be inside the [Gamarr Appdata Directory](/gamarr/appdata-directory)

1. Open config.xml in a text editor
1. Find the authentication method line will be
`<AuthenticationMethod>Basic</AuthenticationMethod>` or `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Change the `AuthenticationMethod` line to `<AuthenticationMethod>None</AuthenticationMethod>`
1. Restart Gamarr
1. Gamarr will now be accessible without a password, you should go the `Settings: General` in the UI and set your username and password

## Weird UI Issues

- If you experience any weird UI issue like the Library page not listing anything or a certain view or sort not working, try viewing in a Chrome Incognito Window or Firefox Private Window. If it works fine there, clear your browser cache and cookies for your specific IP/domain. For more information, see the [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage) wiki article.

## VPNs, Jackett, and the \*ARRs

- Unless you're in a repressive country like China, Australia or South Africa, your torrent client is typically the only thing that needs to be behind a VPN. Because the VPN endpoint is shared by many users, you can and will experience rate limiting, DDOS protection, and ip bans from various services each software uses.
- In other words, putting the \*Arrs (Lidarr, Prowlarr, Radarr, Readarr, Gamarr, and Lidarr) behind a VPN can and will make the applications unusable in some cases due to the services not being accessible.

> **To be clear it is not a matter of if VPNs will cause issues with the \*Arrs, but when: image providers will block you and cloudflare is in front of most of \*Arr servers (updates, metadata, etc.) and liable to block you too**
{.is-warning}

- **Many private trackers will ban you for using or accessing them (i.e. using Jackett or Prowlarr) via a VPN.**

### Use of a VPN

- If a VPN is required and Docker is used it is recommended to use Hotio or Binhex's Download Client + VPN Containers.
- If a VPN is required and Docker is not used your VPN client ***must*** support split tunneling so only the required (Download Client) apps are behind the VPN.
- Many issues with accessing trackers can be resolved by using Google or Cloudflare's DNS servers in place of your ISP's DNS servers.
- In some cases (i.e. UK ISPs) you may need to put your torrent download client behind a VPN and Jackett/Prowlarr as follows:
  - put Jackett behind the VPN and ensure split tunneling allows local access
  - for Prowlarr configure your vpn client to provide a proxy and add the proxy in Settings => Indexers. Give the proxy a tag and any indexers that need to use it the same tag.
    - If absolutely required and if your vpn does not provide a way to create a proxy you can put Prowlarr behind the vpn and ensure split tunneling allows local access.
