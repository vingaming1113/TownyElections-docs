---
description: Nominate candidates, cast ballots, and view results.
icon: person-booth
---

# Run an election

## Run an election

Each election follows four phases: nomination, voting, optional runoff, and conclusion.

### Nomination

Town residents can stand for office during nomination:

```
/election run
/election campaign Build a stronger Oakvale.
```

Candidates can join or create a party with `/election party <name>`. They can leave with `/election party leave`.

By default, campaign details lock when voting begins. Set `campaign.lock-edits-during-voting: false` to allow later edits.

### Vote

Open the election desk with `/election`, or vote from chat:

```
/election vote Alex
```

The ballot syntax depends on the active voting system:

* **Plurality**: choose one candidate.
* **Ranked choice**: list candidates in preference order.
* **Approval**: list every candidate you approve.

For example, `/election vote Alex Mira Rowan` ranks three candidates or approves all three. The active system determines which meaning applies.

{% hint style="info" %}
Each election locks its voting system at startup. Changing the configuration never reinterprets active ballots.
{% endhint %}

### Inspect an election

Use these commands at any time:

```
/election status
/election candidates
/election parties
/election results
```

Live tallies remain hidden when `public-live-results` is `false`.

### Nation elections

Prefix the command with `nation` to act within your nation:

```
/election nation run
/election nation vote Alex
/election nation status
```

Every resident across the nation can nominate and vote. Nation elections require `nation.enabled: true`.
