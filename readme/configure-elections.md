---
description: Configure schedules, ballots, rewards, and integrations.
icon: sliders
---

# Configure elections

## Configure elections

Edit `plugins/TownyElections/config.yml`, then run `/election reload`.

### Core election settings

```yaml
election:
  nomination-duration: "2d"
  voting-duration: "3d"
  min-candidates: 2
  max-candidates: 0
  auto-win-single-candidate: true
  allow-vote-changes: true
  public-live-results: false
  voting-system: "PLURALITY"
  tie-breaker: "INCUMBENT"
```

Durations support `30s`, `10m`, `2h`, `3d`, `1w`, and combinations such as `1w3d12h`. A `max-candidates` value of `0` means unlimited.

Choose one voting system:

* `PLURALITY` — the highest vote total wins.
* `RANKED_CHOICE` — the lowest candidate is eliminated each round.
* `APPROVAL` — the highest approval total wins.

Tie breakers support `RANDOM`, `EARLIEST`, `INCUMBENT`, `RUNOFF`, and `NONE`.

### Winner rewards

Configure Towny ranks, leadership transfers, and server commands under `winner:`.

```yaml
winner:
  set-as-mayor: false
  grant-town-ranks:
    - "councillor"
    - "helper"
  revoke-previous-winner-ranks: true
  commands-on-win:
    - "lp user {winner} parent addtemp mayor 30d"
```

Town ranks must exist in `townyperms.yml`. Invalid ranks are skipped and logged.

Win commands support `{winner}`, `{winner_uuid}`, `{town}`, `{votes}`, `{total_votes}`, and `{winner_party}`. Loss commands also support `{loser}`, `{loser_uuid}`, and `{loser_party}`.

For nation elections, configure `winner.grant-nation-ranks` and `winner.set-as-king`.

### Limit votes by IP

Enable the IP limit to reduce alt-account voting:

```yaml
election:
  ip-vote-limit:
    enabled: true
    max-votes: 1
```

The plugin stores only in-memory SHA-256 fingerprints. It never writes raw IP addresses to logs or disk. Restarting the server resets this tracking.

Shared networks and proxies may share a limit. A player changing IPs can use separate capacity.

### PlaceholderAPI

With PlaceholderAPI installed, use `%townyelections_phase%`, `%townyelections_candidates%`, `%townyelections_votes%`, and `%townyelections_last_winner%`.

Use the `nation_` variant for nation data. For example, `%townyelections_nation_phase%` returns the current nation-election phase.

### Updates and messages

Configure GitHub release checks under `update-checker:`. The plugin checks stable releases only. It never downloads updates automatically.

Edit `messages_en.yml` to customize text and colors. Messages support legacy `&` colors and hex `&#RRGGBB` colors.
