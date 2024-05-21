---
id: helm
title: "Helm"
sidebar_position: 4
---

:::info

**This plugin is available as a part of the Botkube Cloud offering.**

Botkube is introducing new plugins with advanced functionality that will be part of the Botkube Team and Enterprise packages. These advanced plugins require cloud services provided by Botkube and are not part of the Botkube open source software.

As part of this change, some of the existing Botkube plugins are being moved to a new repository. This repository requires authentication with a Botkube account. To continue using these Botkube plugins, create an account at https://app.botkube.io/ and configure a Botkube instance, or [migrate an existing installation with the Botkube CLI](../../cli/migrate.md).

:::


To execute `helm` commands, send message in the following format in the channel where Botkube is already added:

```
@Botkube helm [command] [flags]
```

At least one `helm` executor needs to be enabled and bound to a given channel.


