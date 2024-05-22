---
id: command-aliases
title: Command Aliases
sidebar_position: 4
---

Botkube can define multiple aliases for arbitrary commands. The aliases are replaced with the underlying command before executing it. Aliases can replace a single word or multiple ones. For example, you can define a `k` alias for `kubectl`, or `kgp` for `kubectl get pods`.

Aliases work for all commands, including executor plugins and Botkube built-in ones. To learn more about how to configure Executors, see the [Executor](../self-hosted-configuration/executor/index.md) section.

Aliases are defined globally for the whole Botkube installation. Once they are configured, read the [Aliases](../usage/executor/index.md#aliases) section in Usage document.

## Botkube Cloud

You can configure aliases in the Botkube Cloud dashboard.

1. If you don't have an existing Botkube instance, create a new one, according to the [Installation](../installation/index.mdx) docs.
2. From the [Botkube Cloud homepage](https://app.botkube.io), click the **Aliases** link in the top right corner.
3. Click **Create new** button.
4. Provide display name, alias and command.

   For example, for `exec` plugin, you can provide display name as `Exec alias`, alias as `x`, and command as `exec`.

5. Select instances for which you want to enable the alias.
6. Click **Apply** button.

## Self-hosted Botkube syntax

To configure the aliases for the self-hosted Botkube installation, use the following syntax:

```yaml
# Custom aliases for given commands.
# The aliases are replaced with the underlying command before executing it.
# Aliases can replace a single word or multiple ones. For example, you can define a `k` alias for `kubectl`, or `kgp` for `kubectl get pods`.
#
## Format: aliases.{alias}
aliases:
  kc:
    command: kubectl
    displayName: "Kubectl alias"
  k:
    command: kubectl
    displayName: "Kubectl alias"
## Multi-word alias example:
#  kgp:
#    command: kubectl get pods
#    displayName: "Get pods"
```

The default configuration for Helm chart can be found in the [values.yaml](https://github.com/kubeshop/botkube/blob/main/helm/botkube/values.yaml) file.

## Examples

Alias is a shortcut for a longer command or just a part of it. It can be defined for all commands, including executor plugins and built-in Botkube commands. When you use an alias, the command is replaced with the underlying command before executing it. For example, `@Botkube k get pods` is replaced with `@Botkube kubectl get pods` before executing it.

Once you configured aliases, you can use them interchangeably with a full command. For example:

- `k` as `kubectl`,
- `kgp` as `kubectl get pods`,
- `kgpa` as `kubectl get pods -A`,
- `hh` as `helm history`,
- `a` as `list actions`, the built-in Botkube command,

and so on. Your imagination is the limit!

Aliases are defined globally for the whole Botkube installation. To see which aliases are available for current conversation, run `@Botkube list aliases`.
