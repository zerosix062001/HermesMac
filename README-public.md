# Hermes Mac

Hermes Mac is a native macOS desktop app for running and managing Hermes agents from a polished SwiftUI interface. It is designed for people who keep Hermes on local or remote machines and want a comfortable Mac app for chat, session history, SSH access, approvals, profiles, and skills.

This repository is intended for public app distribution. The application source code is not included here.

## Features

### Native macOS Interface

- SwiftUI app experience built for macOS.
- Split-view layout with a persistent chat/session sidebar.
- Connection tabs for switching between Hermes environments.
- Light and dark mode friendly visual styling.
- Profile-aware themes and avatars.

### Local and SSH Connections

- Connect to a local Hermes installation or a remote Hermes host over SSH.
- Add, edit, and manage multiple SSH connections.
- Uses the normal macOS/OpenSSH stack for authentication.
- Supports `~/.ssh/config`, ssh-agent, Keychain-backed keys, custom SSH users, hosts, ports, and optional key paths.
- Per-connection status indicators for disconnected, connecting, connected, and failed states.

### Chat Sessions

- Start new Hermes chats from the Mac app.
- Resume existing Hermes sessions when remote session IDs are available.
- Select Hermes profiles per connection.
- Chat in a clean bubble interface or switch into terminal chat mode for the same session.
- Pin important chats in the sidebar.
- Refresh remote sessions on demand.
- Load older messages from remote Hermes history.

### Remote History Sync

- Reads Hermes profile and session history from the selected machine.
- Syncs recent sessions for each selected profile.
- Loads message history from Hermes state databases when available.
- Keeps local app state in Application Support so connections, cached sessions, messages, themes, avatars, approvals, and run state survive restarts.

### Other Features

- Built-in terminal view
- Browse skills for the selected connection and profile.
- See installed, missing, active, and disabled skill states.

### Profile Customization

- Per-profile themes.
- Per-profile avatars.
- Quick profile switching from the connection bar.

## Requirements

- macOS 14 Sonoma or newer.
- A working Hermes CLI installation on each local or remote machine you want to control.
- SSH access for remote hosts.
- OpenSSH configured on macOS for remote connections.

For remote hosts, configure SSH the same way you normally would in Terminal. For example:

```sshconfig
Host hermes-vps
  HostName example.com
  User ubuntu
  IdentityFile ~/.ssh/id_ed25519
  AddKeysToAgent yes
  UseKeychain yes
```

Then add that host in Hermes Mac using the same user, host, port, and optional key path.

## How It Works

Hermes Mac delegates authentication and remote access to OpenSSH. It does not manage private keys itself. For chat and history features, the app talks to the Hermes installation on the selected machine and reads Hermes profile, session, skill, and message metadata when those files are available.

## Distribution

Download the latest Hermes Mac app build from this repository's releases page, then move `Hermes Mac.app` to your Applications folder.

If macOS Gatekeeper blocks the app on first launch, open System Settings and allow the app from Privacy & Security, or right-click the app and choose Open.

## Privacy and Security

- Private keys remain on your Mac and are handled by OpenSSH.
- SSH credentials are not bundled into the app.
- Hermes Mac stores local app preferences and cached metadata in your macOS user Application Support directory.
- Remote chat, history, profile, and skill data come from the Hermes installation you connect to.

## Troubleshooting

### SSH Connection Fails

- Confirm the same host works in Terminal with `ssh user@host`.
- Check the configured port, username, hostname, and key path.
- If you rely on `~/.ssh/config`, make sure the app connection values match the host you normally use.
- Make sure your key is loaded into ssh-agent or available through Keychain.

### No Profiles or Sessions Appear

- Confirm Hermes is installed on the target machine.
- Confirm the expected profile directories and state files exist under `~/.hermes`.
- Use Refresh Sessions after changing profiles or remote state.

### Skills Are Missing

- Confirm the selected Hermes profile has skills configured.
- Use the Hermes CLI on the target machine to manage skill enablement:

```sh
hermes skills config
```

## Status

Hermes Mac is under active development. Public releases may change as the Hermes CLI and gateway workflows evolve.
