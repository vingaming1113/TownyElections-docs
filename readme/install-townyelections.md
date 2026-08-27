---
description: Install the plugin and verify that it is ready.
icon: download
---

# Install TownyElections

## Install TownyElections

TownyElections adds configurable town and nation elections to Towny.

### Requirements

Your server needs:

* Paper `1.21.4` or newer
* Java `21` or newer
* Towny `0.100.0.0` or newer

Towny `0.103` is recommended. PlaceholderAPI is optional.

{% stepper %}
{% step %}
### Download the plugin

Download the latest TownyElections JAR from the [release page](https://github.com/vingaming1113/TownyElections/releases).
{% endstep %}

{% step %}
### Install dependencies

Install Towny before starting the server. Confirm your server uses Paper and Java 21.
{% endstep %}

{% step %}
### Start the server

Place the JAR in `plugins/`, then restart the server. TownyElections creates its configuration files in `plugins/TownyElections/`.
{% endstep %}

{% step %}
### Configure and reload

Update `config.yml` and `messages_en.yml` as needed. Run `/election reload` after each change.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
PlaceholderAPI registers TownyElections placeholders automatically when it is installed.
{% endhint %}

### Verify the installation

Join a town as a resident and run `/election`. The election desk opens when the plugin is available.

Administrators can use `/election start` to begin a test election in their town.
