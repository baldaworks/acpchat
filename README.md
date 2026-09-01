# acpchat

[![test](https://github.com/baldaworks/acpchat/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/baldaworks/acpchat/actions/workflows/test.yml)
[![lint](https://github.com/baldaworks/acpchat/actions/workflows/lint.yml/badge.svg?branch=main)](https://github.com/baldaworks/acpchat/actions/workflows/lint.yml)
[![security](https://github.com/baldaworks/acpchat/actions/workflows/security.yml/badge.svg?branch=main)](https://github.com/baldaworks/acpchat/actions/workflows/security.yml)
[![release](https://github.com/baldaworks/acpchat/actions/workflows/omnidist-release.yml/badge.svg)](https://github.com/baldaworks/acpchat/actions/workflows/omnidist-release.yml)
[![npm](https://img.shields.io/npm/v/@baldaworks/acpchat)](https://www.npmjs.com/package/@baldaworks/acpchat)
[![License](https://img.shields.io/github/license/baldaworks/acpchat)](LICENSE)
[![Version](https://img.shields.io/github/v/tag/baldaworks/acpchat?label=version)](https://github.com/baldaworks/acpchat/tags)

**Talk to ACP agents interactively from your terminal.**

`acpchat` starts any stdio Agent Client Protocol (ACP) server command and gives
you a focused terminal chat / REPL for sending prompts, testing sessions, and handling
permission requests.

Use it when you want to try an ACP provider directly before embedding it in an
agent runtime, app, or automation workflow.

## What You Get

| Capability | Behavior |
| --- | --- |
| Interactive ACP chat | Opens a prompt loop against a stdio ACP server command. |
| Session setup | Creates an ACP session before the first user turn. |
| Model selection | Requests a provider model with `--model` when supported. |
| Mode selection | Requests a provider mode with `--mode` when supported. |
| Permission handling | Lets you choose from numbered permission options in the terminal. |
| Quiet lifecycle logs | Keeps output focused unless `--debug` is enabled. |
| Provider agnostic | Works with OpenCode, Codex, Claude Code, Pi, and any executable that speaks ACP over stdio. |

## Try It

Install globally:

```sh
npm install -g @baldaworks/acpchat@latest
```

Run once with `npx`:

```sh
npx @baldaworks/acpchat@latest -- <acp-server-cmd> [args...]
```

Start a chat:

```sh
acpchat -- opencode acp
acpchat --model openai/gpt-5.4 --mode coding -- opencode acp
acpchat --reasoning-effort high -- npx -y @normahq/codex-acp-bridge@latest
acpchat -- npx -y @normahq/codex-acp-bridge@latest
acpchat -- npx -y @zed-industries/claude-code-acp@latest
acpchat --debug -- npx -y pi-acp
```

## Provider Commands

| Provider | Command |
| --- | --- |
| OpenCode | `acpchat -- opencode acp` |
| OpenCode with model/mode | `acpchat --model openai/gpt-5.4 --mode coding -- opencode acp` |
| Codex | `acpchat -- npx -y @normahq/codex-acp-bridge@latest` |
| Codex with reasoning effort | `acpchat --reasoning-effort high -- npx -y @normahq/codex-acp-bridge@latest` |
| Claude Code | `acpchat -- npx -y @zed-industries/claude-code-acp@latest` |
| Pi | `acpchat -- npx -y pi-acp` |
| Generic ACP | `acpchat -- <acp-server-cmd> [args...]` |

The `--` separator is required. Arguments before `--` are treated as
`acpchat` flags; arguments after it are passed to the ACP server command.

## Interaction

- Type a prompt and press Enter to run a turn.
- Type `exit` or `quit` to close the session.
- If ACP permission requests arrive, choose from the numbered options.
- Use `--debug` when you need lifecycle and inspector diagnostics.

## Use Cases

- Smoke-test an ACP provider before wiring it into an ADK or custom runtime.
- Compare model and mode behavior without writing integration code.
- Reproduce provider permission flows from a terminal.
- Debug whether a local ACP command can start, initialize, and complete turns.

## Flags

| Flag | Purpose |
| --- | --- |
| `--model <id>` | Request a session model via ACP `session/set_config_option` config id `model`. |
| `--mode <id>` | Request a session mode via ACP `session/set_config_option` config id `mode`, with legacy `session/set_mode` fallback. |
| `--reasoning-effort <effort>` | Request a session reasoning effort via ACP `session/set_config_option` config id `reasoning_effort`. |
| `--debug` | Enable debug logs. |
| `-h`, `--help` | Show command help. |

Unsupported config option requests fail session setup. Legacy `session/set_mode`
fallback failures are ignored only when the server reports the method as
unsupported.

## Repository

- GitHub: <https://github.com/baldaworks/acpchat>

## Contact

- Issues: <https://github.com/baldaworks/acpchat/issues>
- Maintainer: [@metalagman](https://github.com/metalagman)

## License

MIT. See the repository [LICENSE](https://github.com/baldaworks/acpchat/blob/main/LICENSE).
