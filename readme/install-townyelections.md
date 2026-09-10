---
description: Step-by-step guide to installing TownyElections on your Minecraft server.
---

# Install TownyElections

TownyElections is a Bukkit/Spigot/Paper plugin that runs alongside Towny. Follow these steps to get it up and running.

## Prerequisites

Before installing TownyElections, make sure your server meets the following requirements:

| Requirement | Notes |
|---|---|
| **Server software** | Spigot, Paper, Purpur, or any compatible fork. CraftBukkit is not recommended. |
| **Minecraft version** | Check the plugin download page for the exact supported version range. Recent versions of TownyElections target modern Minecraft releases (1.19+). |
| **Towny** | Towny must already be installed and working. TownyElections is an add-on and will not function without it. |
| **Vault** *(optional but recommended)* | Required if you want to use candidacy fees, vote taxes, or economy-based features. |
| **An economy plugin** *(optional)* | Any Vault-compatible economy plugin (EssentialsX Economy, CMI, etc.) if using economy features. |

## Installation Steps

![Dropping the TownyElections jar into the plugins folder](../assets/install-plugins-folder.png)

### 1. Download the plugin

Download the latest release of TownyElections from the official distribution channel (typically the releases page on the TownyElections repository or the Towny resources page).

Make sure the version you download matches your server's Minecraft version and your installed version of Towny.

### 2. Drop the JAR in your plugins folder

Place the downloaded `TownyElections.jar` file into your server's `plugins/` directory alongside Towny itself.

```
plugins/
├── Towny/
├── TownyElections.jar
└── ...
```

### 3. Start (or restart) your server

Start the server, or restart it if it was already running. TownyElections will:

* Detect that Towny is installed.
* Generate its default configuration file at `plugins/TownyElections/config.yml`.
* Register its commands and permissions.

### 4. Verify the plugin loaded

Once the server finishes starting, run:

```
/version TownyElections
```

If the plugin reports its version correctly, the installation succeeded. You should also see a confirmation message in the server console.

### 5. Configure the plugin

Stop the server, open `plugins/TownyElections/config.yml`, and adjust the settings to match how you want elections to work on your server. See the [Configuration](config.md) page for a full breakdown of every option.

After editing the config, start the server again (or run the reload command if you prefer not to restart).

### 6. Grant permissions

Make sure your players, mayors, nation leaders, and staff have the appropriate permission nodes. See the [Permissions](#permissions) section below for the full list.

## Permissions

TownyElections uses Bukkit permissions to control who can do what. Assign these through your permission plugin (LuckPerms, PermissionsEx, etc.).

| Permission | Description | Default |
|---|---|---|
| `townyelections.vote` | Allows a player to vote in elections they are eligible for. | `true` |
| `townyelections.run` | Allows a player to declare candidacy in an election. | `true` |
| `townyelections.help` | Allows a player to view the TownyElections help menu. | `true` |
| `townyelections.info` | Allows a player to view information about current or upcoming elections. | `true` |
| `townyelections.admin` | Grants access to all administrative commands (start/stop elections, reload, force results). | `op` |
| `townyelections.parties.create` | Allows a player to create a political party (if parties are enabled). | `true` |
| `townyelections.nominate` | Allows a player to nominate another player as a candidate. | `true` |

## Commands

### Player Commands

| Command | Alias | Description |
|---|---|---|
| `/vote` | `/evote` | Open the voting ballot for the current election. |
| `/election info` | `/elections` | View information about current and upcoming elections. |
| `/election run` | `/run` | Declare yourself as a candidate in an open election. |
| `/election withdraw` | | Withdraw your candidacy. |
| `/election candidates` | | View the list of candidates for the current election. |
| `/election results` | | View the results of a past election. |
| `/election help` | | Show the help menu. |

### Admin Commands

| Command | Description | Permission |
|---|---|---|
| `/telection start [town/nation] [name]` | Manually start an election for a town or nation. | `townyelections.admin` |
| `/telection stop [town/nation] [name]` | Cancel a running election. | `townyelections.admin` |
| `/telection reload` | Reload the plugin configuration. | `townyelections.admin` |
| `/telection forcewin [player]` | Force a candidate to win the current election. | `townyelections.admin` |
| `/telection setduration [ticks/minutes/hours]` | Adjust the duration of a running election. | `townyelections.admin` |

## Updating TownyElections

To update to a newer version:

1. Download the new JAR.
2. Stop your server.
3. Replace the old `TownyElections.jar` in your `plugins/` folder with the new one.
4. Start the server. The plugin will automatically migrate your config and data where possible.

{% hint style="warning" %}
Always take a backup of your `plugins/TownyElections/` folder before updating, especially when upgrading across major versions.
{% endhint %}

## Troubleshooting

**Plugin won't enable / says Towny is missing.**
TownyElections requires Towny. Make sure Towny is installed in the `plugins/` folder and has successfully loaded before TownyElections starts.

**Players can't vote.**
Check that:
* An election is currently open for their town or nation.
* They meet the eligibility requirements (residency time, not being a mayor already, etc. — see [Configuration](config.md)).
* They have the `townyelections.vote` permission.

**Elections aren't starting automatically.**
Verify that scheduled elections are enabled in `config.yml` and that the interval is set correctly. Check the server console for any error messages.

**Economy features aren't working.**
Make sure both Vault and a Vault-compatible economy plugin are installed on the server and reload TownyElections.
