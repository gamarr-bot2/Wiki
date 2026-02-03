---
title: Gamarr Settings
description: Description of Gamarr's Settings Menus
published: true
date: 2025-02-02T00:00:00.000Z
tags: settings, configuration, gamarr, profiles, quality, indexers
editor: markdown
dateCreated: 2025-02-02T00:00:00.000Z
---

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Menu options](#menu-options)
- [Media Management](#media-management)
  - [Game Naming](#game-naming)
  - [Folders](#folders)
  - [Importing](#importing)
  - [File Management](#file-management)
  - [Root Folders](#root-folders)
- [Profiles](#profiles)
  - [Quality Profiles](#quality-profiles)
  - [Delay Profiles](#delay-profiles)
  - [Release Profiles](#release-profiles)
- [Quality](#quality)
- [Custom Formats](#custom-formats)
- [Indexers](#indexers)
- [Download Clients](#download-clients)
- [Import Lists](#import-lists)
- [Connect](#connect)
- [Metadata](#metadata)
- [Tags](#tags)
- [General](#general)
- [UI](#ui)

This page will go through all the settings available in Gamarr and how they work. This is not meant to be a comprehensive "how to set up Gamarr." If you want that, please use the [Quick Start](/gamarr/quick-start-guide) page instead.

# Menu options

To get to the Settings page, choose Settings from the sidebar. The following sub-menu options will be available:

- Media Management
- Profiles
- Quality
- Custom Formats
- Indexers
- Download Clients
- Import Lists
- Connect
- Metadata
- Tags
- General
- UI

Also, note that for each individual settings page, there are some options at the top of the menu:

- Hide/Show advanced is important for any items that are marked below as `(Advanced Option)`, otherwise they will not show up. These menu items are shown in orange in the screenshots.

- You must save your changes before leaving the screen. You do that by clicking the disk icon. If you've made no changes, it will show "No Changes" and be grayed out.

# Media Management

> Some of these settings are only visible through `Show Advanced Settings` which is on the top bar under the search bar{.is-info}

## Game Naming

- Rename Games - If unchecked, Gamarr will use the existing name if renaming is disabled
  - If unchecked:
    - Download Client Import
      - Download Client's Release Title is used
    - Manual (Ad-Hoc) Import: Original File Name
- Replace Illegal Characters - If unchecked, Gamarr will remove them instead.
  - The characters are: `:` `\` `/` `>` `<` `?` `*` `|` `"`

## Folders

- Create empty game folders - Create missing game folders during disk scan
- Delete empty folders - Delete empty game folders during disk scan and when game files are deleted

## Importing

- Skip Free Space Check - Use when Gamarr is unable to detect free space from your game root folder
- Minimum Free Space - Toggling this will prevent import if it would leave less than this amount of disk space available
- Use Hard links instead of Copy - Use Hard links when trying to copy files from torrents that are still being seeded
  - For more information on this click [here](https://trash-guides.info/hardlinks)

> You should typically enable this. This will allow you to seed your torrents and not require additional disk space.
{.is-info}

- Import Extra Files - Import matching extra files (nfo, etc) after importing a file

## File Management

- Unmonitor Deleted Games - Games deleted from disk are automatically unmonitored in Gamarr
- Download Proper & Repacks - Whether or not to automatically upgrade to Propers/Repacks
  - Prefer and Upgrade - Rank repacks and propers higher than non-repacks and non-propers. Treat new repacks and propers as upgrade to current releases.
  - Do Not Upgrade Automatically - Rank repacks and propers higher than non-repacks and non-propers. Do not treat new repacks and propers as upgrade to current releases.
  - Do Not Prefer - This effectively ignores repacks and propers. You'll need to manage any preference for those with Custom Formats.

> `PROPER` - means there was a problem with the previous release. Downloads tagged as PROPER shows that the problems have been fixed in that release. This is done by a Group that did not release the original.
> `REPACK` - means there was a problem with the previous release and is corrected by the original Group. Downloads tagged as REPACK shows that the problems have been fixed in that release. This is done by a Group that did release the original.
{.is-info}

- Analyse game files - Extract file information such as resolution, runtime and codec information from files. This requires Gamarr to read parts of the file which may cause high disk or network activity during scans.
- Rescan Game Folder after Refresh - Rescan the game folder after refreshing the game
  - Always - Rescan game folders based on Tasks Schedule
  - After Manual Refresh - You will have to manually rescan the disk
  - Never - Just as it says, never rescan the game folders.
- Change File Date - Change file date on import/rescan
  - None - Gamarr will not change the date that shows in your given file browser
  - Release Date - The date the game was released.
- Recycling Bin - Game files will go here when deleted instead of being permanently deleted
- Recycling Bin Cleanup - This is how old a given file can be before it is deleted permanently

## Root Folders

- Path - This shows the path to your games library
- Free Space - This is the free space being reported to Gamarr from the system
- Unmapped Folders - These are folders that do not have a Game associated with them

> The `X` at the end will remove this root path
{.is-info}

> Note: Root Folders should be where your final organized game files exist, not where downloads go.
{.is-warning}

# Profiles

## Quality Profiles

- Set profiles for the quality of games you're looking to download.

> When selecting an existing profile or adding an additional profile a new window will appear{.is-info}

> Note: The quality which has a blue box is the quality at which any media with this profile will continue to be upgraded to.
{.is-info}

- Plus icon (<kb>+</kb>) - Create a new quality profile

- Name - Select a **UNIQUE** name for the quality profile you are creating
- Upgrades Allowed - When this option is enabled and you tell Gamarr to download a `GOG` and there is a `Steam Rip` in your game library Gamarr will automatically upgrade to the better quality
- Upgrade Until - Once this quality is reached Gamarr will no longer download games

> Note: This is only applicable if you have `Steam Rip` higher than `GOG` within the `Qualities` section
{.is-warning}

- Qualities - Qualities higher in the list are more preferred even if not checked. Qualities within the same group are equal. Only checked qualities are wanted.
  - Edit Groups - Some qualities are grouped together to reduce the size of the list as well as grouping similar releases. Prime example of this is `WebDL` and `WebRip` as these are very similar and typically have similar bitrates. When editing the groups you can change the preference within each of the groups. [See TrAsH's Guide for how to Merge Qualities](https://trash-guides.info/merge-quality)

> By default the qualities are set from lowest (bottom) to highest (top)
{.is-info}

## Delay Profiles

- Delay profiles allow you to reduce the number of releases that will be downloaded for a game by adding a delay while Gamarr continues to watch for releases that better match your preferences.
- Preferred Protocol - This will either be `Usenet` or `Torrent` depending on which download protocol you prefer
- Usenet Delay - Set by the number of minutes you will want to wait before the download to start
- Torrent Delay - Set by the number of minutes you will want to wait before the download to start
- Bypass if Highest Quality - Bypass delay when release has the highest enabled quality profile with the preferred protocol
- Tags - By giving this delay profile a tag you will be able to tag a given game to have it follow the rules set here.
- Wrench icon - This will allow you to edit the delay profile
- Plus icon (<kb>+</kb>) - Create a new delay profile

### Uses

Some media will receive half a dozen different releases of varying quality in the hours after a release, and without delay profiles Gamarr might try to download all of them. With delay profiles, Gamarr can be configured to ignore the first few hours of releases.

Delay profiles are also helpful if you want to emphasize one protocol (Usenet or BitTorrent) over the other.

### How Delay Profiles Work

The timer begins as soon as Gamarr detects a game has a release available. This release will show up in your Queue with a clock icon to indicate that it is under a delay.

> The clock starts from the releases upload time and not from the time Gamarr sees it.
{.is-info}

During the delay period, any new releases that become available will be noted by Gamarr. When the delay timer expires, Gamarr will download the single release which best matches your quality preferences.

The timer period can be different for Usenet and Torrents. Each profile can be associated with one or more tags to allow you to customize which games have which profiles. A delay profile with no tag is considered the default and applies to all games that do not have a specific tag.

> Delay profiles start from the timestamp that the indexer reports the release was uploaded. This means that any content that was published before you enabled the delay profile or added the tag association will not be affected by the delay profile, and will be downloaded immediately. In addition, **any manual searches** for content (non-RSS feed searches) will ignore delay profile settings.
{.is-warning}

## Release Profiles

- Here you will be able to set restrictions on global indexer restrictions based on a few parameters
- Click the <kb>+</kb> and a new window will open
- Must Contain - The release must contain at least one of these terms (case insensitive)
- Must Not Contain - The release will be rejected if it contains one or more of terms (case insensitive)
- Preferred - Here you can select a given term and give it a score.
  - Let's say you are looking for releases with a specific grouping of words. Let's say you want to tell Gamarr that you want Releases with `GOG` over releases that contain `Steam Rip`. Here you would put in your Preferred the term `GOG` and give it a score (say 100).
- Include Preferred when Renaming - Check this box to include your preferred words (or regex matches) in the `{Preferred Words}` file naming token
  - **Note**: only the highest scoring preferred word is included in the file name.
- Indexer - In this drop down you can limit this release profile to a single indexer. This should typically be left at `(Any)`
- Tags - Use a tag here will allow you to apply this release profile to games with the same tag. Leaving this tag blank will have this profile apply to all games

> Release profiles can be either strictly positive (must contain at least one term from the Must Contain list), strictly negative (release will be rejected if it contains one or more of terms from the Must Not Contain list), or both, but the Must Contain list must not be blank.
{.is-info}

# Quality

## Quality Table Meanings

- Quality - The scene quality name (hardcoded)
- Title - The name of the Quality in the GUI (configurable)
- Megabytes Per Minute - Self Explanatory
- Size Limit - Self Explanatory
- Min - The minimum Megabytes per Minute (MB/min) a quality can have.
- Max - The maximum Megabytes per Minute (MB/min) a quality can have.

## Qualities Defined

- Unknown - Self Explanatory
- SDTV - Post air rips from an analog source (usually cable television or OTA standard definition). The image quality is generally good (for the resolution) and they are usually encoded in DivX/XviD or MP4.

# Custom Formats

> Custom Formats can determine which release Gamarr will grab. See [TRaSH's Guide for Custom Formats for Games](https://trash-guides.info) for more details
{.is-info}

- Custom formats allow you to define additional matching criteria beyond quality profiles for game releases.

## Custom Format Conditions

### Conditions

- Release Title - This is a regex matched against the release title and, after download, the filename on disk.
  - Note: Gamarr only uses text after the game title for matching which means anything preceding the title including brackets is ignored.
- Edition - This tag is matched against any editions Gamarr may parse.
- Language - This language is matched against any language(s) Gamarr parses. All languages previously selected in the profile work here.
- Indexer Flag - This condition is matched against any indexer flags that may be parsed.
- Source - The source from where a release was obtained
- Resolution - The resolution parsed from either the release name or mediainfo (if available).
- Quality Modifier - Quality Modifier sets things like `REMUX` etc.
- Size - This is matched against the release size.
- Release Group - This can be used to match a specific release group.

### Profiling Settings and Ranking

- Custom formats are implemented within and have their scores configured at the Quality Profiles level
- The Upgrade Until Custom Format Score value prevents upgrading once a release with this configured score has been downloaded.
- A score of 0 results in the custom format being informational only and has no effect on release ranking nor languages searched for.
- The Minimum Custom Format Score requires releases to reach this threshold otherwise they will be rejected.

> Custom Formats are applied based on their positive or negative scores in the Quality Profile. As such, a Custom Format may be applied in only certain Quality Profiles.
{.is-info}

# Indexers

> Information on supported indexers can be found at the [More Info (Supported)](/gamarr/supported#indexers) page for this section
{.is-info}

## Supported Indexers

- A list of supported indexers is located at the [More Info (Supported)](/gamarr/supported#indexers) page

### Indexer Settings

- Once you've clicked the <kb>+</kb> button to add a new indexer you will be presented with a new window with many different options. For the purposes of this wiki Gamarr considers both Usenet Indexers and Torrent Trackers to be "Indexers".

- There are two sections here: Usenet and Torrents. Based upon what download client you will be using you will want to select the type of indexer you will be going for.

### Usenet Indexer Configuration

- Newznab - Here you will find presets of popular usenet indexers (that are pre-filled out, all you will need is your API key which is provided by the usenet indexer of your choice) along with the ability to create a custom Indexer
- Software that works with Newznab and use newznab as a basis:
  - [Newznab](https://www.newznab.com/)
  - [NZBgeek](https://nzbgeek.info/)
  - [NZBHydra2](https://github.com/theotherp/nzbhydra2)
  - [nZEDb](https://github.com/nZEDb/nZEDb)
  - [Prowlarr](/prowlarr)

### Torrent Tracker Configuration

- Torznab - This indexer type is used with Prowlarr and Jackett. Additional presets are available for widely used tracker software.

## Options

- Minimum Age - Usenet only: Minimum age in minutes of NZBs before they are grabbed. Use this to give new releases time to propagate to your usenet provider.
- Retention - Usenet only: Set to zero to set for unlimited retention
- Maximum Size - Maximum size for a release to be grabbed in MB. Set to zero to set to unlimited. Please note that this applies globally.
- Prefer Indexer Flags - Prioritize releases with special flags.
- Availability Delay - Amount of time before (-#) or after (#) the release date to search for the game.
- RSS Sync interval - Interval in minutes. Set to zero to disable (this will stop all automatic release grabbing) Minimum: 10 minutes Maximum: 120 minutes

> If Gamarr has been offline for an extended period of time, Gamarr will attempt to page back to find the last release it processed in an attempt to avoid missing a release. As long as your indexer supports paging and it hasn't been too long Gamarr will be able to process the releases it would have missed and avoid you needing to perform a search for the missed games.{.is-info}

# Download Clients

> Information on supported download clients can be found at the [More Info (Supported)](/gamarr/supported#download-clients) page for this section
{.is-info}

## Overview

- Downloading and importing is where most people experience issues. From a high level perspective, the software needs to be able to communicate with your download client and have access to the files it downloads. There is a large variety of supported download clients and an even bigger variety of setups. This means that while there are some common setups there isn't one right setup and everyone's setup can be a little different. But there are many wrong setups.

## Download Clients

- Once you click the <kb>+</kb> button you will be presented with a new window that will give you the option of many different download clients. Gamarr supports many download clients and strives to support any client that it can effectively use.

## Supported Download Clients

- A list of supported download clients is located at the [More Info (Supported)](/gamarr/supported#download-clients) page

## Completed Download Handling

- Completed Download Handling is how Gamarr imports media from your download client to your series folders. Many common issues are related to bad Docker paths and/or other Docker permissions issues.

- Enable - Automatically import completed downloads from the download client
- Remove - Remove completed downloads when finished (usenet) or stopped/complete (torrents)

## Remote Path Mappings

- Remote Path Mapping acts as a dumb find Remote Path and replace with Local Path. This is primarily used for either merged local/remote setups using mergerfs or similar or is used for when the application and download client are not on the same server.

# Import Lists

> Information on supported list types can be found at the [More Info (Supported)](/gamarr/supported#lists) page for this section
{.is-info}

## Lists

- Import lists are a part of Gamarr that allow you to follow a given list creator. Let's say that you follow a given Steam curator and really like their games and want to add every game on their list. You look in your Gamarr and realize that you do not have those games. Well instead of searching one by one and adding those items and then searching your indexers for those games. You can do this all at once with a List. The Lists can be set to import all games on that curator's list as well as be set to automatically assign a quality profile, automatically add, and automatically monitor that game.

## List Exclusions

- List Exclusion - This allows you to prune your list of games you do not wish to ever see again. An example of this is if your list happens to contain a game that is in a foreign language and it is not likely for you to ever find this game in your native language and do not want to download it with subtitles. You can exclude a game from ever being added in the future.

# Connect

> Information on supported connection types can be found at the [More Info (Supported)](/gamarr/supported#notifications) page for this section
{.is-info}

## Connections

Connections are how you want Gamarr to communicate with the outside world.

- By pressing the <kb>+</kb> button you will be presented with a new window which will allow you to configure many different endpoints

- A list of supported notifications & connections is located at the [More Info (Supported)](/gamarr/supported#notifications) page

## Connection Triggers

- On Grab - Be notified when games are available for download and has been sent to a download client
- On Import - Be notified when games are successfully imported
- On Upgrade - Be notified when games are upgraded to a better quality
- On Rename - Be notified when games are renamed
- On Game Delete - Be notified when games are deleted
- On Game File Delete - Be notified when games files are deleted
- On Game File Delete For Upgrade - Be notified when game files are deleted for upgrades
- On Health Issue - Be notified on health check failures
- Include Health Warnings - Be notified on health warnings in addition to errors.
- On Application Update - Be notified when Gamarr gets updated to a new version

# Metadata

## Metadata Consumers

- Here you can select the type of metadata that will be consumed by your media player

- Kodi will be one of the most commonly used options here if that is the software being used. This will allow Gamarr to create a NFO file as well as associated game posters to be scraped into your player

# Tags

- The tag section in Gamarr is used to link different aspects of Gamarr.
- Tags are particularly useful for:
  - Delay Profiles
  - Release Profiles
  - Indexers
- Tags can be used to link Delay Profiles, Release Profiles, Indexers, and Games together.
- For Example:
  - You only want a specific indexer to be used for a specific game. You would create a tag and assign the game and indexer that tag.
  - You want a specific Release Profile to only use a specific Delay Profile. You would create a tag and assign the Release Profile and Delay Profile that tag.

# General

## Host

- Bind Address - Valid IPv4 address or '*' for all interfaces
  - 0.0.0.0 or `*` - any address can connect
  - 127.0.0.1 or localhost - only localhost applications can connect
  - Any other IP (e.g. 1.2.3.4) - only that IP (1.2.3.4) can connect
- Port Number - The port number that you are wanting to use to access the webUI for Gamarr

> Note: If using Docker do not touch this setting.
{.is-warning}

- URL Base - For reverse proxy support, default is empty

> Note: If using a reverse proxy (example: mydomain.com/gamarr) you would enter '/gamarr' for URL Base.
{.is-info}

- Instance Name - Instance name in tab and for Syslog app name

> If you run multiple instances, this will add the instance name to the browser tab name. {.is-info}

- Enable SSL - If you have SSL credentials and would like to secure communication to and from your Gamarr enable this option.

> Note: Do not use this unless you know what you're doing.
{.is-warning}

## Security

- Authentication - How would you like to authenticate to access your Gamarr instance
  - As of today, 2025-02-02, Authentication is now required. See the required [Authentication FAQ Entry](/gamarr/faq#forced-authentication) for details.
  - None - You have no authentication to access your Gamarr. Typically if you're the only user of your network, do not have anyone on your network that would care to access your Gamarr or your Gamarr is not exposed to the web
  - Basic (Browser pop-up) - This option when accessing your Gamarr will show a small pop-up allowing you to input a Username and Password
  - Forms (Login Page) - This option will have a familiar looking login screen much like other websites have to allow you to log onto your Gamarr
- API Key - This is how other programs would communicate or have Gamarr communicate with other programs. This key if given to the wrong person with access could do all kinds of things to your library. This is why in the logs the API key is redacted
- Certificate Validation - Change how strict HTTPS certificate validation is
  - Enabled - Validate all HTTPS certificates (recommended)
  - Disabled for Local Addresses - Validate all HTTPS certificates except those on localhost and the LAN
  - Disabled - Do not validate any HTTPS certificates

## Proxy

- Proxy - This option allows you to run your Gamarr through a proxy. This may be required if your ISP blocks connections to certain sites. You may need to configure your client to go through this proxy.

## Logging

- Log level - Probably one of the most useful troubleshooting tools
  - Info - This is the most basic way that Gamarr gathers information this will include very minimal amount of information in the logs. This log file contains fatal, error, warn and info entries.
  - Debug - Debug will include all the information that Info includes plus more information that can be useful. This log files contains fatal, error, warn, info and debug entries
  - Trace - The most advance and detailed logging on Gamarr, Trace will include all the information gathered by Info and Debug and more. This is the most common type of log that is going to be asked for when troubleshooting on Discord or Reddit. If you're needing help please select your log to Trace and redo the task that was giving you problems to capture the log. This log files contains fatal, error, warn, info, debug and trace entries.

## Analytics

- Analytics - Send anonymous usage and error information to Gamarr's servers (Servarr). This includes information on your browser, which Gamarr WebUI pages you use, error reporting as well as OS and runtime version. We will use this information to prioritize features and bug fixes.

## Updates

- (Advanced Option) Branch - This is the branch of Gamarr that you are running on.
  - [Please see this FAQ entry for more information](/gamarr/faq#how-do-i-update-gamarr)
- Automatic - Automatically download and install updates. You will still be able to install from System: Updates. Note: Windows Users are always automatically updated.
- Mechanism - Use Gamarr's built-in updater or a script
  - Built-in - Use Gamarr's own updater
  - Script - Have Gamarr run the update script
  - Docker - Do not update Gamarr from inside the Docker, instead pull a brand new image with the new update
- Script - Visible only when Mechanism is set to Script - Path to update script
- Update Process - Gamarr will download the update file, verify its integrity and extract it to a temporary location and call the chosen method. The update process will be run under the same user that Gamarr is run under, it will need permissions to update the Gamarr files as well as stop/start Gamarr.
- Built-in - The built-in method will backup Gamarr files and settings, stop Gamarr, update the installation and Start Gamarr, if your system will not handle the stopping of Gamarr and will attempt to restart it automatically it may be best to use a script instead. In the event of failure, the previous version of Gamarr will be restarted.
- Script - The script should handle the same as the built-in updater, if you need to handle stopping and starting services (upstart/launchd/etc) you will need to do that here.

## Backups

- The backup section allows you to tell Gamarr how you would like for it to handle backups

- Folder - This allows you to select the backup location. In Docker this will be limited to what you allow the container to see. Paths are relative to the appdata folder; if necessary, you can set an absolute path to backup outside of the appdata folder.
- Interval - How often would you like Gamarr to make a backup
- Retention - How long would you like Gamarr to hold on to each backup. After a new backup is made the oldest backup will be removed

# UI

## Calendar

- First Day of Week - Here you can select what you think the first day of the week should be.
- Week Column Header - Here you can select the header for the columns

## Games

- Run Time Format - Select how you want run times to be formatted from showing hours only to minutes

## Dates

- Short Date Format - How do you want Gamarr to display short dates?
- Long Date Format - How do you want Gamarr to display long format dates?
- Time Format - Do you want a 12hr or 24hr format?
- Show Relative Dates - Do you want Gamarr to show relative (Today/Yesterday/etc) or absolute dates?

## Style

- Enable Color-Impaired Mode - Altered style to allow color-impaired users to better distinguish color coded information

## Language

- UI Language - Select the Language for Gamarr to use within the application UI
