---
title: Gamarr Library
description: Manage your game collection, monitor status, and organize game library in Gamarr
published: true
date: 2025-02-02T00:00:00.000Z
tags: gamarr, library, games, management, collection, organization
editor: markdown
dateCreated: 2025-02-02T00:00:00.000Z
---

# Games

## Library View

- Update All - Update metadata for all games, refresh posters, rescan game folders, and rescan game files (if enabled)
- Refresh & Scan - Refresh the currently viewed game's metadata and rescan its folder
- RSS Sync - Refresh the RSS feed from your Indexers and see if anything new has been posted to be grabbed
- Search All / Search Filtered / Search Selected - Search all games or selected games in the current view
- Manual Import (Game Index) - Manually import a game file for a game you have added to Gamarr from any folder that Gamarr can access
  - Move Automatically - Automatically attempt to match a file to a Game in Gamarr and import by moving it.
  - Interactive Import - Review all files within the path and attempt to match to a Game in Gamarr allowing the user to review the results. Move or Copy/Hardlink is a selectable option in the bottom left corner.
- Manual Import (Game) - Manually import a game file for a game you have added to Gamarr from the assigned game's folder
  - Move Automatically - Automatically attempt to match a file to a Game in Gamarr and import by moving it.
  - Interactive Import - Review all files within the path and attempt to match to a Game in Gamarr allowing the user to review the results. Move or Copy/Hardlink is a selectable option in the bottom left corner.
- Game Editor / Game Index - Toggle between Mass Editor mode and Game Index (Library) mode
- Options - Change display options
- View - Toggle View Type
  - Table - Tabular View (list view)
  - Posters - Display Posters (similar to Plex)
  - Overview - Display overview information and the poster (detailed view)
- Sort - Sort the current view

### Filters

- Filter - Filter the current view
  - Monitored Only - Titles being monitored for updates.
  - Unmonitored - Titles NOT being monitored for updates.
  - Missing - In the database, monitored, but missing from the filesystem.
  - Wanted - In the database, monitored, missing, but should be available based on the availability settings
  - Cut-off Unmet - Title on filesystem, but still monitoring for wanted quality.
  - Custom Filters
    - Monitored (boolean)
    - Title \[contains\] (String)
    - Release Status (Enum)
    - Quality Profile (Enum QualityProfiles)
    - Added (static DateTime, relative TimeDelta)
    - Year (Int)
    - Path \[contains\] (String)
    - Size on Disk (Int)
    - Genres \[contains\] (Enum Genres)
    - Tags \[contain\] (Enum Tags)

# Add New

- If you're looking to add a new game, this is the page that you will be wanting to do that from.
  - You'll find the how-to in our [Quick Start Guide](/gamarr/quick-start-guide).
- Below the search field, you can also find the Import Existing Games button. If that is the case for you, you can find great information on that also in our [Quick Start Guide](/gamarr/quick-start-guide).

# Library Import

Library Import allows you to import existing organized games and each game's file via existing files in the path directory. This is especially useful when making a new Gamarr instance and wanting to keep your existing games.

- Library import is for adding and importing an existing organized library of games into Gamarr.
- Library Import cannot be used for:
  - Importing files from a download folder
  - Adding or Importing one or more files that are not properly named and organized in their own Game Folder within your root folder or a folder you wish to add as a root folder
  - Any other uses that are not adding a game to Gamarr and importing the game and its file from the root (library) folder that was input to Library Import

> \* Non-Windows: If you're using an NFS mount ensure `nolock` is enabled.
> \* If you're using an SMB mount ensure `nobrl` is enabled.
{.is-warning}

> **The user and group you configured Gamarr to run as must have read & write access to this location.** {.is-info}

> Library import does not and should not be used for:
>
> - Importing files from your download folder
> - Adding or Importing one or more game files that are not properly named and organized in their own game subfolder within your root folder or a folder you wish to add as a root folder
{.is-warning}

# Discover

The Discover feature allows you to find new games based on:

- Your existing library
- Popular games
- Recently released games
- Games from specific platforms

You can filter and sort the discovered games by various criteria before adding them to your library.

# Collections

Collections allow you to organize your games into custom groups. This is useful for:

- Organizing games by franchise
- Grouping games by platform
- Creating custom lists for different purposes

To create a collection, navigate to Library => Collections and click the + button.
