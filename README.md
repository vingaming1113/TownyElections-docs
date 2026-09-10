---
description: Hold democratic elections for Mayor and Nation Leader positions in Towny.
---

# TownyElections

TownyElections is an add-on plugin for [Towny](https://townyadvanced.github.io/) that adds democratic elections to your Minecraft server. With TownyElections, towns and nations can vote on who should lead them instead of leadership being handed down by the previous leader or set manually by staff.

When an election is called, residents (or nation members, depending on the election type) receive ballot access and can cast their votes for any valid candidate. When the voting period ends, the candidate with the most votes is automatically sworn in as Mayor or Nation Leader.

## Key Features

* **Mayor elections** — Let a town's residents vote on who becomes Mayor.
* **Nation Leader elections** — Let nation members vote on who runs the nation.
* **Scheduled & on-demand elections** — Run elections on a fixed schedule or start them manually with a command.
* **Candidacy system** — Players can declare their candidacy before an election opens.
* **Configurable voting periods** — Control how long elections last, who is eligible to vote, and how often they run.
* **Political parties** *(if enabled)* — Group candidates into parties with platforms and party-based voting.
* **Built-in economy support** — Optionally require a candidacy fee or refund votes through Vault.
* **Towny permission integration** — Respects Towny's permission nodes and resident/nation ranks.

## How it Works

1. An election is scheduled or started by an admin, or triggered automatically when a leader steps down.
2. Players who meet the requirements (residency, playtime, etc.) can declare themselves as candidates.
3. When voting opens, eligible voters can run `/vote` (or the configured command) to open the ballot.
4. After the voting window closes, the plugin tallies the votes and announces the winner.
5. The winner is automatically assigned the Mayor or Nation Leader role through Towny.

## Next Steps

* [Install TownyElections](readme/install-townyelections.md) — Get the plugin running on your server.
* [Configuration](readme/config.md) — Tune election timing, eligibility, and economy settings.
* [Voting](readme/voting.md) — How candidates run and players vote.
