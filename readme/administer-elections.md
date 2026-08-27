---
description: Start, manage, and automate town or nation elections.
icon: user-gear
---

# Administer elections

## Administer elections

Administrators manage elections with `townyelections.admin`. This permission defaults to server operators.

### Manage a town election

```
/election start [town]
/election stop [town]
/election cancel [town]
/election reload
```

Without a town name, the command targets your current town. Administrators can target another town by name.

`stop` closes voting and counts ballots immediately. `cancel` ends the election without selecting a winner.

### Manage a nation election

Use the `nation` prefix to target a nation:

```
/election nation start [nation]
/election nation stop [nation]
/election nation cancel [nation]
```

Without a nation name, the command targets your current nation.

### Permissions

* `townyelections.candidate` — run or manage a campaign.
* `townyelections.vote` — cast a ballot.
* `townyelections.info` — view election information.
* `townyelections.admin` — manage elections and reload configuration.
* `townyelections.*` — grant every permission.

The candidate, vote, and info permissions default to `true`.

### Automate recurring elections

Enable `election.auto-schedule.enabled` to start recurring town elections. Set `election.auto-schedule.interval` to a duration such as `30d`.

Nation elections can use the same cadence. Enable `nation.auto-schedule` and `nation.enabled`.

### Election outcomes

When voting ends, TownyElections counts ballots, resolves ties, records results, and applies winner rewards. Active elections and stored results survive restarts in `data.yml`.
