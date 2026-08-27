---
description: Build, test, and submit improvements to TownyElections.
icon: code-pull-request
---

# Contribute to TownyElections

## Contribute to TownyElections

Contributions are welcome. Keep each change focused and easy to review.

### Before you start

You need Java `21` and Maven. Use a Paper `1.21.4+` test server with Towny installed to verify runtime behavior.

Start with an [existing issue](https://github.com/vingaming1113/TownyElections/issues) when one matches your work. Open an issue first for larger features or behavior changes.

### Build the plugin

{% stepper %}
{% step %}
### Clone your fork

Fork the repository, then clone your fork locally. Add the main repository as `upstream` if you want to pull future changes.
{% endstep %}

{% step %}
### Create a branch

Create a branch from the current `main` branch. Use a short descriptive name, such as `fix-nation-ballot`.
{% endstep %}

{% step %}
### Package the project

Run the following command from the repository root:

```bash
mvn clean package
```

Maven resolves the Paper API, Towny, and PlaceholderAPI dependencies declared by the project.
{% endstep %}

{% step %}
### Test the JAR

Copy the shaded JAR from `target/` into your test server’s `plugins/` directory. Start the server and test the affected workflow.
{% endstep %}
{% endstepper %}

### Validate your change

Test the full election path when your change affects voting or outcomes:

1. Start an election and nominate candidates.
2. Cast valid and invalid ballots.
3. End voting and verify results and winner rewards.

Also restart the server during an active election when persistence changes. Confirm the election resumes correctly.

### Submit a pull request

1. Rebase or merge the latest `main` changes.
2. Run `mvn clean package` successfully.
3. Push your branch and open a pull request.

Use a clear title that describes the user-facing change. Explain why it is needed, how you tested it, and any configuration changes. Link the related issue when applicable.

{% hint style="info" %}
Do not include generated build files, test-server data, or unrelated formatting changes.
{% endhint %}

### Report issues

Use the [issue tracker](https://github.com/vingaming1113/TownyElections/issues) for bugs and feature ideas.

Include your TownyElections version, Paper version, Towny version, Java version, and relevant console errors. Add exact reproduction steps when possible.

### Documentation and configuration changes

Update `config.yml` comments when you add or change an option. Update `messages_en.yml` when behavior needs a new player-facing message.

Document new commands, permissions, placeholders, and winner placeholders in this site. Keep terminology consistent with Towny and the existing command syntax.

### License

TownyElections uses the [MIT License](https://github.com/vingaming1113/TownyElections/blob/main/LICENSE). Contributions are provided under the same license.
