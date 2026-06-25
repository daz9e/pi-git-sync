# pi-git-sync

Pi package that adds `/sync` to sync `~/.pi/agent` through Git.

It keeps your Pi config portable across machines without committing auth, sessions, caches, package clones, or local sync state.

## Install

```bash
pi install npm:pi-git-sync
```

Then run inside Pi:

```text
/sync <git-repo-url>
```

After the first setup, use:

```text
/sync
```

## Commands

```text
/sync <repo>   # configure repo and sync
/sync          # sync configured repo
/sync status   # show git status
```

## What gets synced

- `settings.json`
- `web-search.json`
- `keybindings.json`
- `agents/`
- `extensions/`
- `skills/`
- `prompts/`
- `themes/`

## What is ignored

- `auth.json`
- `models.json`
- `sync.json`
- `sessions/`, `cache/`, `logs/`, `tmp/`
- `npm/`, `git/`, `node_modules/`
- `.env`, tokens, credentials, keys, pem files

## Conflict handling

If Git reports a conflict, `/sync` offers to:

- ask the agent to merge
- abort
- use local and force-push
- use remote and backup local

When the agent resolves a conflict, the next `/sync` commits it as:

```text
sync: agent merged conflicts ...
```

## Safety

- Uses an allowlist instead of `git add .`.
- Refuses to commit staged files that look like secrets.
- Backs up local config before replacing it with remote config.
- Generates the config repo `README.md` automatically.

## Development

```bash
npm run smoke
```

## License

MIT
