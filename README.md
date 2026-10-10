# Opportune Agent releases

Downloads for the **Opportune Agent**, the desktop companion to
[Opportune](https://opportune.haseebarshad.com). The agent pairs with your
Opportune server, fills job applications in a browser on your own computer, and
runs your own AI (Claude Code, Ollama, LM Studio, or your API keys). Nothing
here contains account data. The source lives in a private repository.

Get the files from the [latest release](https://github.com/Haseeb-Arshad-Dev/opportune-releases/releases/latest).

| Platform | File | Notes |
| --- | --- | --- |
| macOS (Apple silicon and Intel) | `Opportune-Agent-<version>-mac-universal.dmg` | Not notarized yet; see [Opening on macOS](#opening-on-macos). |
| Linux | `Opportune-Agent-<version>-linux-x86_64.AppImage` | Run `chmod +x` on it, then run it. It updates itself. |
| Debian / Ubuntu | `opportune-agent_<version>_amd64.deb` | Install with `sudo apt install ./opportune-agent_<version>_amd64.deb`. |
| Headless (servers, terminals) | `opportune-agent-cli-<version>.tar.gz` | Needs Node.js 22.12 or newer. Unpack it, then run `node opportune-agent.mjs --help`. |

Each release lists a SHA-256 checksum for every file.

## Opening on macOS

The macOS build is not yet signed with an Apple Developer ID, so the first time
you open it macOS says it "could not verify" the app is free of malware.

1. Drag the app into Applications and open it once. On the warning, click **Done**.
2. Open **System Settings → Privacy & Security**. Scroll to **Security** and
   click **Open Anyway** next to the message about the agent, then confirm with
   your password or Touch ID and click **Open**.

Or, in Terminal: `xattr -dr com.apple.quarantine /Applications/*Opportune*.app`

You only need to do this once per version. (Right-click → Open no longer
bypasses this on macOS 15 and later.)

## Pair it

1. In Opportune, open **Settings → Agents → Pair an agent** and copy the code.
2. Desktop app: paste the code when the app asks for it. CLI:

   ```bash
   node opportune-agent.mjs pair --server https://your-opportune-server --code XXXX-XXXX --name my-laptop
   node opportune-agent.mjs install-service --yes   # systemd --user on Linux, launchd on macOS
   node opportune-agent.mjs doctor
   ```

The agent submits an application only after you approve it in Opportune,
unless you turn on auto-submit yourself. It never solves captchas, and it
hands sign-ins and bot checks back to you.
