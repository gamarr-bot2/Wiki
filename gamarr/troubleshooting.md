---
title: Gamarr Troubleshooting
description: Troubleshooting for Gamarr including getting log files, search troubleshooting and common problems, and downloading / importing troubleshooting and common problems
published: true
date: 2025-02-02T00:00:00.000Z
tags: gamarr, troubleshooting
editor: markdown
dateCreated: 2025-02-02T00:00:00.000Z
---

# Asking for Help

Do you need help? That's okay, everyone needs help sometimes. You can get real time help via chat on

- [<i class="fab fa-discord"></i>&emsp;Discord *Official Gamarr Discord*](https://discord.gg/gamarr)
{.links-list}

But before you go there and post, be sure your request for help is the best it can be. Clearly describe the problem and briefly describe your setup, including things like your OS/distribution, version of .NET, version of Gamarr, download client and its version. **If you are using [Docker](https://www.docker.com/) please run through [Docker Guide](/docker-guide) first as that will solve common and frequent path/permissions issues. Otherwise please have a [docker compose](/docker-guide#docker-compose) handy. [How to Generate a Docker Compose](https://trash-guides.info/compose)** Tell us about what you've tried already, what you've looked at. Use the [Logging and Log Files section](#logging-and-log-files) to turn your logging up to trace, recreate the issue, pastebin the relevant context and include a link to it in your post. Maybe even include some screen shots to highlight the issue.

The more we know, the easier it is to help you.

# Logging and Log Files

It is likely beneficial to also review the Common Troubleshooting problems:

- [Downloads and Importing Common Problems](#common-problems)
- [Searching Indexers and Trackers Common Problems](#common-problems-1)
{.links-list}

If you're asked for debug logs your logs will contain `debug` and if you're asked for trace logs your logs will contain `trace`. If the logs you are providing do not contain either then they are not the logs requested.

- Avoid sharing the entire log file unless asked.
- Don't upload logs directly to Discord or paste them as walls of text, unless requested.
- Don't share the logs as an attachment, a zip archive, or anything other than text shared via the services noted below

To provide good and useful logs for sharing:

> Ensure a spammy task is NOT running such as an RSS refresh
{.is-warning}

1. [Turn Logging up to Trace (Settings => General => Log Level or Edit The Config File)](#tracedebug-logs)
2. [Clear Logs (System => Logs => Clear Logs or Delete all the Logs in the Log Folder)](#clearing-logs)
3. Reproduce the Issue (Redo what is breaking things)
4. [Open the trace log file (gamarr.trace.txt) via the UI or the log file](#standard-logs-location) on the filesystem and find the relevant context
5. Copy a big chunk before the issue, the issue itself, and a big chunk after the issue.
6. Use [Gist](https://gist.github.com/), [0bin (**Be sure to disable colorization**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/), or similar sites - excluding those noted to avoid below - to share the copied logs from above

**Warnings:**

- **Do not use [pastebin.com](https://pastebin.com) as their filters have a tendency to block the logs.
- Do not use [pastebin.pl](https://pastebin.pl) as their site is frequently not accessible.
- Do not use [JustPasteIt](https://justpaste.it/) as their site does not facilitate reviewing logs.
- Do not upload your log as a file
- Do not upload and share your logs via Google Drive, Dropbox, or any other site not noted above.
- Do not archive (zip, tar (tarball), 7zip, etc.) your logs.
- Do not share console output, docker container output, or anything other than the application logs specified

**Important Note:**

- When using [0bin](https://0bin.net/), be sure to disable colorization and do not burn after reading.

- Alternatively If you're looking for a specific entry in an old log file but aren't sure which one you can use N++. You can use the Notepad++ "Find in Files" function to search old log files as needed.
- **Unix Only:** Alternatively If you're looking for a specific entry in an old log file but aren't sure which one you can use grep. For example if you want to find information about the game "Elden Ring" you can run the following command `grep -inr -C 100 -e 'Elden Ring' /path/to/logs/*.trace*.txt` If your [Appdata Directory](/gamarr/appdata-directory) is in your home folder then you'd run: `grep -inr -C 100 -e 'Elden Ring' /home/$User/.config/logs/*.trace*.txt`

```none

    * The flags have the following functions
    * -i: ignore case
    * -n: show line number
    *  -r: recursively check all files in the path
    * -C: provide # of lines before and after the line it is found on
    * -e: the pattern to search for

```

## Standard Logs Location

The log files are located in Gamarr's [Appdata Directory](/gamarr/appdata-directory), inside the logs/ folder. You can also access the log files from the UI at System => Logs => Files.

> Note: The Logs ("Events") Table in the UI is not the same as the log files and isn't as useful. If you're asked for logs, please copy/paste from the log files and not the table.
{.is-info}

## Update Logs Location

The update log files are located in Gamarr's [Appdata Directory](/gamarr/appdata-directory), inside the UpdateLogs/ folder.

## Sharing Logs

The logs can be long and hard to read as part of a forum or Reddit post and they're spammy in Discord, so please use [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net), or any other similar pastebin site. The whole file typically isn't needed, just a good amount of context from before and after the issue/error. Do not forget to wait for spammy tasks like an RSS sync or library refresh to finish.

## Trace/Debug Logs

You can change the log level at Settings => General => Logging. Gamarr does not need to restarted for the change to take effect. This change only affects the log files, not the logging database. The latest debug/trace log files are named `gamarr.debug.txt` and `gamarr.trace.txt` respectively.

If you're unable to access the UI to set the logging level you can do so by editing config.xml in the AppData directory by setting the LogLevel value to Debug or Trace instead of Info.

```xml
 <Config>
   [...]
   <LogLevel>debug</LogLevel>
   [...]
 </Config>
```

## Clearing Logs

You can clear log files and the logs database directly from the UI, under System => Logs => Files and System => Logs => Delete (Trash Can Icon)

# Multiple Log Files

Gamarr uses rolling log files limited to 1MB each. The current log file is always `gamarr.txt`, for the other files `gamarr.0.txt` is the next newest (the higher the number the older it is). This log file contains `fatal`, `error`, `warn`, and `info` entries.

When Debug log level is enabled, additional `gamarr.debug.txt` rolling log files will be present. This log file contains `fatal`, `error`, `warn`, `info`, and `debug` entries. It usually covers about a 40h period.

When Trace log level is enabled, additional `gamarr.trace.txt` rolling log files will be present. This log files contains `fatal`, `error`, `warn`, `info`, `debug`, and `trace` entries. Due to trace verbosity it only covers a couple of hours at most.

# Recovering from a Failed Update

- We do everything we can to prevent issues when upgrading, but they occur, this will walk you through the steps of recovering your installation.

## Determine the issue

- The best place to look when the application will not start after an update is to review the [update logs](#update-logs-location) and see if the update completed successfully. If those do not have an issue then the next step is to look at your regular application log files, before trying to start again, use [Logging](/gamarr/settings#logging) and [Log Files](/gamarr/system#log-files) to find them and increase the log level.
- **Migration Issue** - Migration errors will not be identical, but here is an example.

## Resolving the issue

In the event of a migration issue there is not much you can do immediately, if the issue is specific to you (or there are not yet any posts), please create a post on our Discord. If there are others with the same issue, then rest assured we are working on it.

> Please ensure you did not try to use a database from `nightly` on the stable version. Branch hopping is ill-advised.{.is-info}

### Permissions Issues

- Fix the permissions to ensure the user/group the application is running as can access (read and write) to both `/tmp` and the Installation Directory of the application.

### Manually upgrading

Grab the latest release from our GitHub.

Install the update (.exe) or extract (.zip) the contents over your existing installation and re-run Gamarr as you normally would.

# Downloads and Importing

Downloading and importing is where *most* people experience issues. From a high level perspective, Gamarr needs to be able to communicate with your download client and have access to the files it downloads. There is a large variety of supported download clients and an even *bigger* variety of setups. This means that while there are some *common* setups, there isn't one *right* setup and everyone's setup can be a little different.

> **The first step is to turn logging up to Trace, see [Logging and Log Files](#logging-and-log-files) for details on adjusting logging and searching logs. You'll then reproduce the issue and use the trace level logs from that time frame to examine the issue.**
> If someone is helping you, put context from before/after in a [pastebin](https://0bin.net), [Gist](https://gist.com), or similar site to show them.
> It doesn't need to be the entire file and it shouldn't *just* be the error. You should also reproduce the issue while tasks that spam the log file are not running.
{.is-danger}

When you reach out for help, be sure to read [asking for help](#asking-for-help) so that you can provide us with the details we'll need.

## Testing the Download Client

Ensure your download client(s) are running. Start by testing the download client, if it doesn't work you'll be able to see details in the trace level logs. You should find a URL you can put into your browser and see if it works. It could be a connection problem, which could indicate a wrong IP, hostname, port or even a firewall blocking access. It might be obvious, like an authentication problem where you've gotten the username, password or apikey wrong.

## Testing a Download

Now we'll try a download. Pick a game and do a manual search. Pick one of those files and attempt to download it. Does it get sent to the download client? Does it end up with the correct category? Does it show up in Activity? Does it end up in the trace level logs during the **Check For Finished Download** task (Refresh Monitored Downloads and Process Monitored Downloads tasks) which runs roughly every minute? Does it get correctly parsed during that task? Does the queued up download have a reasonable name? Since searches are by ID on some indexers/trackers, it can queue one up with a name that it can't recognize.

## Testing an Import

Import issues should almost always manifest as an item in Activity with an orange icon you can hover to see the error. If they're not showing in Activity, this is the issue you need to focus on first so go back and figure that out. Most import errors are *permissions* issues, remember that Gamarr needs to be able to read and write in the download folder. Sometimes, permissions in the library folder can be at fault too, so be sure to check both.

Incorrect path issues are possible too, though less common in normal setups. The key to understanding path issues is knowing that Gamarr gets the path to the download *from* the download client, via its API. This becomes a problem in more unique use cases, like the download client running on a different system (maybe even OS\!). It can also occur in a Docker setup, when volumes are not done well. A remote path map is a good solution where you don't have control, like a seedbox setup. On a Docker setup, fixing the paths is a better option.

## Common Problems

Below are some common problems.

### Download Client's WebUI is not enabled

Gamarr talks to your download client via its API and accesses it via the client's webui. You must ensure the client's webui is enabled and the port it is using does not conflict with any other client ports in use or ports in use on your system.

### SSL in use and incorrectly configured

Ensure SSL encryption is not turned on if you're using both your instance and your download client on a local network. See [the SSL FAQ entry](/gamarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) for more information.

### Can't see share on Windows

The default user for a Windows service is `LocalService` which typically doesn't have access to your shares. Edit the service and set it up to run as your own user, see the FAQ entry [why can't I see my files on a remote server](/gamarr/faq#why-can-gamarr-not-see-my-files-on-a-remote-server) for details.

### Mapped network drives are not reliable

While mapped network drives like `X:\` are convenient, they aren't as reliable as UNC paths like `\\server\share` and they're also not available before login. Setup and your download client(s) so that they use UNC paths as needed. If your library is on a share, you'd make sure your root folders are using UNC paths. If your download client sends to a share, that is where you'll need to configure UNC paths since Gamarr gets the download path from the download client. It is fine to keep your mapped network drives to use yourself, just don't use them for automation.

### Docker and user, group, ownership, permissions and paths

Docker adds another layer of complexity that is easy to get wrong, but still end up with a setup that functions, but has various problems. Instead of going over them here, read this wiki article [for these automation software and Docker](/docker-guide) which is all about user, group, ownership, permissions and paths. It is not specific to any Docker system, instead it goes over things at a high level so that you can implement them in your own environment.

### Remote Path Mapping

If you have Gamarr in Docker and the Download Client in non-Docker (or vice versa) or have the programs on different servers then you may need a remote path map.

Logs will look like

```none
2025-02-01 01:01:23.5|Error|DownloadedGameImportService|Import failed, path does not exist or is not accessible by Gamarr: /volume1/games/Elden Ring/EldenRing.zip. Ensure the path exists and the user running Gamarr has the correct permissions to access this file/folder
```

Thus `/volume1/games` does not exist or is not accessible within Gamarr's container.

- [Settings => Download Clients => Remote Path Mappings](/gamarr/settings#remote-path-mappings)
- A remote path mapping is used when your download client is reporting a path for completed data either on another server or in a way that Gamarr doesn't address that folder.
- Generally, a remote path map is only required if your download client is on Linux when Gamarr is on Windows or vice versa. A remote path map is also possibly needed if mixing Docker and Native clients or if using a remote server.

### Permissions on the Library Folder

Logs will look like

```none
2025-02-01 01:01:23.5|Error|DownloadedGameImportService|Import failed, path does not exist or is not accessible by Gamarr: /games/Elden Ring. Ensure the path exists and the user running Gamarr has the correct permissions to access this file/folder
```

Don't forget to check permissions and ownership of the *destination*. It is easy to get fixated on the download's ownership and permissions and that is *usually* the cause of permissions related issues, but it *could* be the destination as well. Check that the destination folder(s) exist. Check that a destination *file* doesn't already exist or can't be deleted or moved to recycle bin. Check that ownership and permissions allow the downloaded file to be copied, hard linked or moved. The user or group that runs as needs to be able to read and write the root folder.

- For Windows Users this may be due to running as a Service:
  - the Windows Service runs under the 'Local Service' account, by default this account does not have permissions to access your user's home directory unless permissions have been assigned manually. This is particularly relevant when using download clients that are configured to download to your home directory.
  - 'Local Service' also generally has very limited permissions. It's therefore advisable to install the app as a system tray application if the user can remain logged in. The option to do so is provided during the installer. See the FAQ for how to convert from a service to tray app.

- For Synology Users refer to [SynoCommunity's Permissions Article for their Packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Non-Windows: If you're using an NFS mount ensure `nolock` is enabled.
- If you're using an SMB mount ensure `nobrl` is enabled.

### Permissions on the Downloads Folder

Logs will look like

```none
2025-02-01 01:01:23.5|Error|DownloadedGameImportService|Import failed, path does not exist or is not accessible by Gamarr: /downloads/Elden Ring. Ensure the path exists and the user running Gamarr has the correct permissions to access this file/folder
```

Don't forget to check permissions and ownership of the *source*. It is easy to get fixated on the destination's ownership and permissions and that is a *possible* cause of permissions related issues, but it *typically* is the source. Check that the source folder(s) exist. Check that ownership and permissions allow the downloaded file to be copied/hard linked or copy+delete/moved. The user or group that runs as needs to be able to read and write the downloads folder.

- For Windows Users this may be due to running as a Service:
  - the Windows Service runs under the 'Local Service' account, by default this account does not have permissions to access your user's home directory unless permissions have been assigned manually. This is particularly relevant when using download clients that are configured to download to your home directory.
  - 'Local Service' also generally has very limited permissions. It's therefore advisable to install the app as a system tray application if the user can remain logged in. The option to do so is provided during the installer. See the FAQ for how to convert from a service to tray app.

- For Synology Users refer to [SynoCommunity's Permissions Article for their Packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Non-Windows: If you're using an NFS mount ensure `nolock` is enabled.
- If you're using an SMB mount ensure `nobrl` is enabled.

### Download folder and library folder not different folders

- The download client should download into a folder accessible by Gamarr and that is not your root/library folder; Gamarr should import from that separate download folder into your Library folder.
- You should never download directly into your root folder. You also should not use your root folder as the download client's completed folder or incomplete folder.
- [**This will also cause a health check in System as well**](/gamarr/system#downloading-into-root-folder)
- Within the application, a root folder is defined as the configured media library folder. This is not the root folder of a mount. Your download client has an incomplete or complete (or is moving completed downloads) into your root (library) folder. This frequently causes issues and is not advised. To fix this change your download client so it is not placing downloads within your root folder. Note that 'placing' also includes if your download client category is set to your root folder or if NZBGet/SABnzbd have sort enabled and are sorting to your root folder. Please note that this check looks at all defined/configured root folders added not only root folders currently in use. In other words, the folder your download client downloads into or moves completed downloads to, should not be the same folder you have configured as your root/library/final media destination folder in the \*Arr application.
- Configured Root Folders (aka Library folders) can be found in [Settings => Media Management => Root Folders](/gamarr/settings/#root-folders)
- One example is if your downloads are going into `\data\downloads` then you have a root folder set as `\data\downloads`.
- It is suggested to use paths like `\data\media\` for your root folder/library and `\data\downloads\` for your downloads.

### Incorrect category

Gamarr should be setup to use a category so that it only tries to process its own downloads. It is rare that a torrent submitted without the correct category, but it can happen. If you're adding torrents manually and want to process them, they'll need to have the correct category. It can be set at any time, since Gamarr attempts to process downloads every minute.

### Packed torrents

Logs will indicate errors like

```none
No files found are eligible for import
```

If your torrent is packed in `.rar` files, you'll need to setup extraction. We recommend [Unpackerr](https://github.com/unpackerr/unpackerr) as it does unpacking right: preventing corrupt partial imports and cleans up the unpacked files after import.

The error may also be seen if there is no valid media file in the folder.

### Repeated downloads

There are a few causes of repeated downloads, but one is related to Custom Formats. It's possible the release name matches a custom format, but the download files do not. This gets you into a loop where you download the items again and again because it looks like an upgrade, then isn't, then shows up again and looks like an upgrade, then isn't. Depending on your custom format you may be able to work around this by including the custom format in your renaming schema. (Enable the Custom Format to be included in renaming then add Custom Format to your renaming schema)

This may also be due to the fact that the download never actually imports then is missing from the queue, so a new download is perpetually grabbed and never imported. Please see the various other common problems and troubleshooting steps for this.

### Usenet download misses import

Gamarr only looks at the 60 most recent downloads in SABnzbd and NZBGet, so if you *keep* your history this means that during large queues with import issues, downloads can be silently missed and not imported. The best way to avoid that is to keep your history clear, so that any items that still appear need investigating. You can achieve this by enabling Remove under Completed and Failed Download Handler. In NZBGet, this will move items to the *hidden* history which is great. Unfortunately, SABnzbd does not have a similar feature. The best you can achieve there is to use the nzb backup folder.

### Download client clearing items

The download client should *not* be responsible for removing downloads. The Usenet client should be configured so it *doesn't* remove downloads from history. The torrent client should be setup so it *doesn't* remove torrents when they're finished seeding (pause or stop instead). This is because Gamarr communicates with the download client to know what to import, so if they're *removed* there is nothing to be imported. even if there is a folder full of files.

For SABnzbd, this is handled with the History Retention setting.

### Download cannot be matched to a library item

For various reasons, releases cannot be parsed once grabbed and sent to the download client. Activity => Options => Show Unknown (this is now enabled by default in recent builds) will display all items not otherwise ignored / already imported within Gamarr's download client category. These will typically need to be manually mapped and imported.

Reasons include:

- Game name has a `:` in it and metadata source doesn't have a search result when searching using the `:` or an alternate name without one. See [this issue](https://github.com/gamarr-app/Gamarr/issues) for more details.
- File name is missing the year which is required for identification

This can also occur if you have a release in your download client but that game (id in the database) has been deleted from the application.

### The underlying connection was closed: An unexpected error occurred on a send

This is caused by the indexer using an SSL protocol not supported by the current .NET version found in [Gamarr => System => Status](/gamarr/system#status).

### The request timed out

Gamarr is getting no response from the client.

```none
    System.NET.WebException: The request timed out: 'https://example.org/api?b]televis]televis'
```

```none
    System.NET.WebException: The request timed out: 'https://example.org/api?b]televis]televis'
```

```none
    System.NET.WebException: The request timed out: 'https://example.org/api?b]televis]televis'
```

This can be caused by an improperly configured reverse proxy, .NET 6 update issues, or sporadically by cloudflare.

### Cannot assign requested address

```none
WARN Load [<module>]: Can't assign requested address: 'http://url:port/' at System.Net.HttpListener.AddAllPrefixes()
```

Try closing any related processes that may be using the port, or use a different port.

# Searches Indexers and Trackers

- [Why didn't Gamarr grab a game I was expecting?](/gamarr/faq#why-didnt-gamarr-grab-a-game-i-was-expecting)
- The [Gamarr Supported](/gamarr/supported) page is the definitive list of supported components
- [Prowlarr](/prowlarr) is a first party Servarr indexer/tracker manager that integrates seamlessly with all \*Arr apps and supports both Usenet and Torrents

## Queries are sent too frequently

{#searches-indexers-and-trackers-queries-are-sent-too-frequently}

- The Search Flow and Timing is driven by RSS Sync.
- Gamarr uses an intelligent algorithm to find releases. The algorithm starts at the low end of the quality profile and works up testing the best release at each quality level.
  - In short, searches are for title only.
- If grabbing from RSS is enabled then any time RSS runs (at the RSS Interval), new uploads are processed. If an upgrade is found that upgrade is grabbed.

## Jackett's /all Endpoint

{#jackett-all-endpoint}

- The Jackett `/all` endpoint is convenient, but that is its only benefit. Everything else is potential problems, so adding each tracker individually is required. Alternatively, you may wish to check out the Jackett & NZBHydra2 alternative [Prowlarr](/prowlarr)
- **February 2025 Update: \*Arr Support has ceased for the jackett `/all` endpoint. Jackett /all endpoint is no longer supported (e.g. warnings will appear) as of 2025-02-11 because it only causes issues.**

- Using the jackett /all endpoint is not recommended, even jackett advises it should not be used.
- Using the /all endpoint has no advantages, only disadvantages:
  - you lose control over indexer specific settings (categories, search modes, etc.)
  - mixing search modes (IMDB, query, etc.) might cause low-quality results
  - indexer specific categories (\>= 100000) cannot be used.
  - slow indexers will slow down the overall result
  - total results are limited to 1000
  - if one of the trackers in /all returns an error, \*Arr will disable it and now you do not get any results.

### Jackett /All Solutions

- Add each tracker in Jackett manually as an indexer in \*Arr
- Check out [Prowlarr](/prowlarr) which can sync indexers to \*Arr and is from the Lidarr/Radarr/Readarr development team.
- Check out [NZBHydra2](https://github.com/theotherp/nzbhydra2) which can sync indexers to \*Arr. But do not use their single aggregate endpoint and use `cat` and `category` instead if the sync will be used.

## Common Problems

- [Game not found in search / No Results](/gamarr/faq)

Below are some common problems.

### Media is Unmonitored

The game(s) is(are) not monitored.

### Tracker Needs RawSearch Capabilities

- Gamarr is searching for `Elden Ring` but your tracker only has results for `Elden.Ring`.
  - This is caused by your tracker not supporting normal standardized searches.
- The solution is that your tracker's definition's search capabilities need to be updated to indicate it [requires and supports `RawSearch`](https://github.com/Prowlarr/Prowlarr/issues/399)
- Jackett supports the flag, but the capabilities need to be updated on a per-indexer basis. Open a feature request for Jackett to add this functionality for your indexer.
- Prowlarr supports the flag, but the capabilities need to be updated on a per-indexer basis. Open a feature request for Prowlarr to add this functionality for your indexer.

### Wrong categories

Incorrect categories is probably the most common cause of results showing in manual searches of an indexer/tracker, but *not* in \*Arr. The indexer/tracker *should* show the category in the search results, which should help you figure out what is missing. If you're using Jackett or Prowlarr, each tracker has a list of specifically supported categories. Make sure you're using the correct ones for Categories. Many find it helpful to have the list visible in one browser window while they edit the entry in.

### Wrong results

Sometimes indexers will return completely unrelated results; Gamarr will feed in parameters to limit the search to a game. Sometimes the returned results are completely unrelated. Or sometimes, mostly related with a few incorrect results. The first is usually an indexer problem and you'll be able to tell from the trace logs which is causing it. You can disable that indexer and report the problem. The other is usually categorized releases which should be reportable on the indexer/tracker.

### Missing Results

If you have results on the site you can find that are not showing in Gamarr then your issue is likely one of several possibilities:

- [Categories are incorrect - See Above](#wrong-categories)
- An ID (TMDbId, IMDbId, etc.) based searched is being done and the indexer does not have the releases correctly mapped to that ID. This is something only your indexer can solve. They need to ensure the release is mapped to the correct applicable IDs.
- Not searching how Gamarr searches; It's highly likely the terms you are searching on the indexer is not how Gamarr queries it. You can see how Gamarr queries from the Trace Logs. Text based queries will generally be in the format of `q=words%televis%here%televis%televis` this string is HTTP encoded and can be easily decoded using any HTML decoding/encoding tool online.
- [See the FAQ for how Gamarr searching works](/gamarr/faq#how-does-gamarr-find-games)

### Certificate validation

You'll be connecting to most indexers/trackers via https, so you'll need that to work properly on your system. That means your time zone and time both need to be set *correctly*. It also means your system certificates need to be up to date.

### Hitting rate limits

If you run your through a VPN or proxy, you may be competing with 10s or 100s or 1000s of other people all trying to use services like , theXEM, and/or your indexers and trackers. Rate limiting and DDOS protection are often done by IP address and your VPN/proxy exit point is *one* IP address. Unless you're in a repressive country like China, Australia or South Africa you don't need to VPN/proxy .

Rarbg has a tendency to have some sort of rate limiting within their API and displays as responding with no results.

### IP Ban

Similarly to rate limits, certain indexers - such as Nyaa - may outright ban an IP address. This is typically semi-permanent and the solution is to get a new IP from your ISP or VPN provider.

### Year Doesn't Match

- This release looks like a good release, but the year is wrong so we're not grabbing it.
  - The Year in the release does not match the year of your game

### Missing Year

- The release will not be grabbed because the release name does not contain a year and we're configured to require a year.
  - The release does not contain a year, so it is skipped based on settings

### Using the Jackett /all endpoint

- The Jackett `/all` endpoint is convenient, but that is its only benefit. Everything else is potential problems, so adding each tracker individually is now required.
- [Even Jackett's Devs says it should be avoided and should not be used.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Using the /all endpoint has no advantages, only disadvantages:
  - you lose control over indexer specific settings (categories, search modes, etc.)
  - mixing search modes (IMDB, query, etc.) might cause low-quality results
  - indexer specific categories (\>= 100000) cannot be used.
  - slow indexers will slow down the overall result
  - total results are limited to 1000
  - unrelated results
  - missing results

## Errors

These are some of the common errors you may see when adding an indexer

### The underlying connection was closed: An unexpected error occurred on a send

This is caused by the indexer using an SSL protocol not supported by the current .NET version found in [Gamarr => System => Status](/gamarr/system#status).

### The request timed out

Gamarr is getting no response from the indexer.

```none
    System.NET.WebException: The request timed out: 'https://example.org/api?b]televis]televis'
```

```none
    System.NET.WebException: The request timed out: 'https://example.org/api?b]televis]televis'
```

```none
    System.NET.WebException: The request timed out: 'https://example.org/api?b]televis]televis'
```

This can be caused by an improperly configured reverse proxy, .NET 6 update issues, or sporadically by cloudflare.
