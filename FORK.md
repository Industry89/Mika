# About this fork

This is a fork of [wangzan101/Mika](https://github.com/wangzan101/Mika) with one change: the
`phone_system_command` tool is removed.

Upstream, that tool lets the model run any Android shell command (shell UID) without
confirmation, and sandbox commands can reach it through the `mika phone` bridge. Because Mika
reads untrusted content (web pages, chats, app screens), a prompt injection could use it to
install apps, grant permissions or change system settings. With the tool unregistered, neither
the model nor sandbox commands can call it. The shell helper itself still runs, because Mika
needs it to work on its virtual display.

Everything else is unchanged.

## Builds

`.github/workflows/build.yml` builds a release APK on every push to `main` and publishes it to
the `latest` release. It is signed with this fork's own key, so:

- It can't be installed over the official Mika app (different signature). Uninstall that first.
- Mika's in-app updater offers official releases, but they are rejected (signer mismatch).
  Update by installing the next build from this fork's `latest` release.

Unit tests are not run in CI: upstream's prompt snapshot tests expect the removed tool.
