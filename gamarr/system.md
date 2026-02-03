---
title: Gamarr System
description: System information, logs, scheduled tasks, and status monitoring for Gamarr administration and troubleshooting
published: true
date: 2025-02-02T00:00:00.000Z
tags: system, administration, logs, tasks, status, gamarr
editor: markdown
dateCreated: 2025-02-02T00:00:00.000Z
---

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Status](#status)
  - [Health](#health)
    - [System Warnings](#system-warnings)
    - [Download Clients](#download-clients)
    - [Indexers](#indexers)
    - [Game Folders](#game-folders)
  - [Disk Space](#disk-space)
  - [About](#about)
  - [More Info](#more-info)
- [Tasks](#tasks)
  - [Scheduled](#scheduled)
  - [Queue](#queue)
- [Backup](#backup)
- [Updates](#updates)
- [Events](#events)
- [Log Files](#log-files)

# Status

## Health

- This page contains a list of health checks errors. These health checks are periodically performed by Gamarr and on certain events. The resulting warnings and errors are listed here to give advice on how to resolve them.

### System Warnings

#### Branch is not a valid release branch

- The branch you have set is not a valid release branch. You will not receive updates. Please change to one of the current release branches.

#### Currently installed SQLite version is not supported

- Gamarr stores its data in an SQLite database. The SQLite library installed on your system is not supported. Gamarr requires at least version 3.9.0.

#### Database Failed Integrity Check

- Your database failed an integrity check. There may be a problem with your database. Please see [our troubleshooting guide](/gamarr/troubleshooting) for more information.

#### New update is available

- Rejoice, the developers have released a new update. This generally means awesome new features and squashed piles of bugs (right?). If you don't have Auto-Updating enabled you will have to figure out how to update on your platform. Pressing the Install button on the System => Updates page is probably the safest starting point.

> This warning will not appear if your current version is less than 14 days old
{.is-info}

#### Cannot install update because startup folder is not writable by the user

- This means Gamarr will be unable to update itself. You'll have to update Gamarr manually or set the permissions on Gamarr's Startup directory (the installation directory) to allow Gamarr to update itself.

#### Could not connect to signalR

- signalR drives the dynamic UI updates, so if your browser cannot connect to signalR on your server you won't see any real-time updates in the UI.
- The most common occurrence of this is use of a reverse proxy or cloudflare.
- Cloudflare needs websockets enabled.

##### Nginx

- Nginx requires the following addition to the location block for the app:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Make sure you do not include proxy_set_header Connection "Upgrade"; as suggested by the nginx documentation. THIS WILL NOT WORK
> See <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache2

For Apache2 reverse proxy, you need to enable the following modules: proxy, proxy_http, and proxy_wstunnel. Then, add this websocket tunnel directive to your vhost configuration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:6969/$1 [P,L]
```

##### Caddy

For Caddy (V1) use this:
Note: you will also need to add the websocket directive to your gamarr configuration

```none
 proxy /gamarr 127.0.0.1:6969 {
     websocket
     transparent
 }
```

### Download Clients

#### No download client is available

- A properly configured and enabled download client is required for Gamarr to be able to download media. Since Gamarr supports different download clients, you should determine which best matches your requirements. If you already have a download client installed, you should configure Gamarr to use it and create a category. See Settings => Download Client.

#### Unable to communicate with download client

- Gamarr was unable to communicate with the configured download client. Please verify if the download client is operational and double-check the URL. This could also indicate an authentication error.
- This is typically due to an improperly configured download client. Things you can typically check:
  - Your download client's IP Address - if it's all on the same bare metal machine this is typically `127.0.0.1`
  - The Port number that your download client is using - these are filled out with the default port number, but if you've changed it you'll need to have the same one entered into Gamarr.
  - Ensure SSL encryption is not turned on if you're using both your Gamarr instance and your download client on a local network (i.e. over plain HTTP). See the SSL FAQ entry for more information.

#### Download clients are unavailable due to failure

- One or more of your download clients is not responding to requests made by Gamarr. Therefore, Gamarr has decided to temporarily stop querying the download client on its normal 1-minute cycle, which is normally used to track active downloads and import finished ones. However, Gamarr will continue to attempt to send downloads to the client, but will in all likelihood fail.
- You should inspect System => Logs to see what the reason is for the failures.
- If you no longer use this download client, disable it in Gamarr to prevent the errors.

#### Enable Completed Download Handling

- Gamarr requires Completed Download Handling to be able to import files that were downloaded by the download client. It is recommended to enable Completed Download Handling. (Completed Download Handling is enabled by default for new users.)

### Indexers

#### No indexers available with automatic search enabled, Gamarr will not provide any automatic search results

- Simply put you do not have any of your indexers set to allow automatic searches.
- Go into Settings => Indexers, select an indexer you'd like to allow Automatic Searches and then click save.

#### No indexers available with RSS sync enabled, Gamarr will not grab new releases automatically

- Gamarr uses the RSS feed to pick up new releases as they come along. [See the FAQ for more information](/gamarr/faq#how-does-gamarr-work)
- To correct this issue go to Settings => Indexers, select an indexer you have and enable RSS Sync.

#### No indexers are enabled

- Gamarr requires indexers to be able to discover new releases. Please read the wiki on instructions on how to add indexers.

### Game Folders

#### Missing Root Folder

- This error is typically identified if a game is looking for a root folder but that root folder is no longer available.
- This error may also be if a list is still pointed at a root folder but that root folder is no longer available.
- If you would like to remove this warning simply find the game that is still using the old root folder and edit it to the correct root folder.

## Disk Space

- This section will show you available disk space.
- In docker this can be tricky as it will typically show you the available space within your Docker image.

## About

- This will tell you about your current install of Gamarr.

## More Info

- Home Page: Gamarr's home page (GitHub)
- Wiki: You're here already.
- Discord: Join the discord
- Donations: If you're feeling generous and would like to donate click here.
- Source: GitHub
- Feature Requests: Got a great idea drop it here.

# Tasks

## Scheduled

- This page lists all scheduled tasks that Gamarr runs

- Application Check Update - This will run every on the displayed schedule in the UI, checking to see if Gamarr is on the most current version then triggering the update script to update Gamarr. Settings => Update

> Note: If on Docker this will not update your container as a new image will need to be downloaded.
{.is-warning}

- Backup - This will run a backup of your Gamarr's database on a set schedule more details on this can be found here. More information about backups can be found at System => Backups.
- Check Health - Check Health will run on the displayed schedule in the UI checking the overall health of your Gamarr. To see a list of possible health related issues see the Wiki Entry on Health Checks.
- Housekeeping - On the displayed schedule in the UI this will dust out all the cobwebs, sweeps and vacuums the floors, mops, shines, and even makes nice neat little folded notes just for you. But does not take out the trash. That it just was not paid enough for.
- Import List Sync - On the displayed schedule in the UI this will run your Lists and import any possible new games. More info about lists can be found at Settings => Lists.
- Messaging Cleanup - On the displayed schedule in the UI this cleans up those messages that appear in the bottom left corner of Gamarr.
- Refresh Monitored Downloads - This goes through and refreshes the downloads queue located under Activity. Essentially pinging your download client to check for finished downloads.
- Refresh Game - This goes through and refreshes all the metadata for all monitored and unmonitored games.
- RSS Sync - This will run the RSS Sync. This can be changed in settings => Indexers => options. More information on the RSS function can be found on our FAQ.

> All these tasks can be ran manually outside their scheduled times by hitting the icon to the far right of each of the tasks.
{.is-info}

## Queue

- The queue will show you running and upcoming tasks as well as a history of recently ran tasks and how long those tasks took.

# Backup

> If you're looking for how to back/restore your Gamarr instance click [here](/gamarr/faq#how-do-i-backuprestore-gamarr).
{.is-info}

- Within the Backup section you will be presented with previous backups (unless you have a fresh install that hasn't made any backups).

- Backup Now - This option will trigger a manual backup of your Gamarr's database.
- Restore Backup - This will open a new screen to restore from a previous backup.
  - By selecting Choose File this will prompt your browser to open a dialog box to restore from a Gamarr Zip backup.

- If you have any previous backups and would like to download them from Gamarr to be placed in a non-standard location you simply can select one of these files to download them.
- Off to the right of each of the previous download you have two options.
  - Restore (Clock Icon) - To restore from a previous backup - This will open a new window to confirm you want to restore from this backup.
  - Delete (Trashcan) - To delete a previous backup.

# Updates

- The update screen will show the past 5 updates that have been made as well as the current version you are on.
- This page will also display the update notes from the Developers telling you what has been fixed or added to Gamarr (Rejoice!)

> A Maintenance Release contains bug fixes and other various improvements. Take a look at the commit history on GitHub for specifics.
{.is-info}

# Events

- The events tab will show you what has been happening within your Gamarr. This can be used to diagnose some light issues. However, this does not replace Trace Logs discussed in Logging.

> Events are the equivalent of INFO Logs. {.is-info}

- Components - This column will tell you what component within Gamarr has been triggered.
- Message - This column will tell you what message has been sent from the component from the previous column.
- Gear Icon - This option will allow you to change how many Components/Messages are displayed per page (Default is 50).
- Options at the top of the page
  - Refresh - This option will refresh the current page, pulling a new events log.
  - Clear - This will clear the current events log allowing you to start from fresh.

# Log Files

- This page will allow you to download and see what current log files are available for Gamarr.

- On the top row there are several options to allow you to control your log files.

- The top row on the far left there is a dropdown that will allow you to switch from Log files and Updater Log Files.
  - Log Files - The bread and butter of any support issue more on log files can be found here.
  - Updater Log Files - This will show the log files associated with Gamarr's updater script.

> If you're on docker this will be empty as you should be updating by downloading a new docker image.
{.is-info}

- Refresh - This will refresh the current page and display any newly created logs.
- Delete - This will clear all logs allowing you to start from fresh.
- File Name - This will display the file name associated with the log.
- Last Written - This is the local time that this particular log file was written to.
  - Gamarr uses rolling log files limited to 1MB each. The current log file is always gamarr.txt, for the other files gamarr.0.txt is the next newest (the higher the number the older it is). This log file contains `fatal`, `error`, `warn`, and `info` entries.
  - When Debug log level is enabled, additional gamarr.debug.txt rolling log files will be present. This log file contains `fatal`, `error`, `warn`, `info`, and `debug` entries. It usually covers about a 40h period.
  - When Trace log level is enabled, additional gamarr.trace.txt rolling log files will be present. This log files contains `fatal`, `error`, `warn`, `info`, `debug`, and `trace` entries. Due to trace verbosity it only covers a couple of hours at most.
