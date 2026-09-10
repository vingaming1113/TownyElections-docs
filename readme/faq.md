---
description: Frequently asked questions about TownyElections.
---

# FAQ

Common questions from server owners, players, and candidates.

![A player asking a question to another player holding a book](../assets/faq-chat.png)

## For Server Owners

**Does TownyElections work with Towny advanced permission setups?**
Yes. TownyElections hooks directly into Towny's resident and nation member data, so it respects your existing rank and permission setup.

**Can I disable elections for a specific town or nation?**
Yes — you can disable elections on a per-town or per-nation basis using admin commands, or disable nation/mayor elections entirely in the config.

**What happens to the current Mayor/Nation Leader when an election is won?**
The previous leader is automatically demoted to a regular resident (or nation member). They are not kicked out of the town or nation. The winner is immediately assigned the leadership role.

**Can I run elections manually instead of on a schedule?**
Absolutely. Set `interval-days` to `0` in the relevant section of `config.yml`, and start elections manually with `/telection start`.

**Is there a way to see past election results?**
Yes. Use `/election results [town/nation] [name]` to see past results. Elections are stored in the database for as long as configured (`keep-results-days` in `config.yml`).

**Does TownyElections work with Folia?**
Check the release notes for your specific version. Many recent Towny add-ons support Folia, but compatibility varies by build.

**How do I prevent alt-account voting?**
Set `one-vote-per-ip: true` under `voter-requirements`, and consider raising `min-playtime-hours` and `min-residency-days` so newly created accounts cannot immediately swing an election.

## For Players

**How do I know if there's an election happening?**
You will receive a chat message when the candidacy phase opens, when voting begins, and periodic reminders if you haven't voted yet. You can also run `/election info` at any time to check.

**Can I vote for myself if I'm a candidate?**
Yes, you are allowed to cast a vote for yourself unless the server has specifically configured otherwise.

**Do I have to be online at the exact moment voting ends?**
No. As long as you submit your vote at any point during the voting phase, your vote will be counted.

**Can I run for both Mayor and Nation Leader at the same time?**
Depending on server configuration, this may or may not be allowed. Check with your server admin. In many setups you can run for both, but you will have to choose one if you win both.

**My vote didn't go through / I got an error. What do I do?**
First, confirm you meet the voting requirements (playtime, residency days, etc.) by re-reading the server's election rules. If you believe you're eligible and still can't vote, contact a server admin — there may be a plugin conflict or configuration issue.

**Is there a way to see who I voted for after submitting?**
By default, votes are anonymous (see `public-votes` in the config). If public votes are enabled, your vote may be visible; otherwise, you will not be able to retrieve your selection once submitted.

## Troubleshooting Quick Reference

| Problem | Things to Check |
|---|---|
| Plugin won't enable | Is Towny installed and loaded? Check console for errors. |
| Elections aren't starting | Is `enabled: true`? Is the `interval-days` set to a value greater than 0? Check console for errors on startup. |
| Players can't run | Check `candidate-requirements` — playtime, residency, fee (if economy enabled). |
| Economy isn't working | Install Vault and a Vault-compatible economy plugin, then restart. |
| Party commands don't work | Set `parties.enabled: true` in config and reload. |
| Results seem incorrect | Check the `voting-system.type` setting — plurality, runoff, and IRV produce very different outcomes. |
