# Claude stop talking like >that<

A skill for Claude Code that stops it from burying the answer. Action first. Steps numbered. No "Hope this helps!"

Forked from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd). I don't have adhd and feel weird about claiming I do, so I trimmed down the adhd-specific language. The original repo also is compatible for many harnesses, here it is stripped to just a bare Claude Code plugin — see [Credits](#credits).

## What changes

<table>
<tr>
<td width="50%">

## Before

> Great question! Let me think about this. Your auth flow has a few moving pieces: the middleware, the token verification, and the cookie handling. Looking at `src/auth.ts`, the `verifyToken` function (around lines 42-58) seems to be using an older `jsonwebtoken` API. One approach would be to update the package and rewrite that function. After making the change, you'd want to run the auth tests to confirm nothing breaks. By the way, you might also want to look at your dependency versions overall. Hope this helps! Let me know if you want to dig deeper.

</td>

<td width="50%">

## After

> Run `npm install jsonwebtoken@latest`, then edit `src/auth.ts:42`.
>
> 1. Open `src/auth.ts`
> 2. Replace `verifyToken` (lines 42–58) with the snippet below
> 3. Run `npm test -- auth.spec.ts`
>
> Next: paste the first failing line if any test fails.

</td>
</tr>
</table>

## The rules

10 rules. Full text in [SKILL.md](./skills/claude-stop-talking-like-that/SKILL.md).

1. Lead with the next action.
2. Number multi-step tasks.
3. End with one concrete next step.
4. Suppress tangents.
5. Restate state every turn.
6. Specific time estimates (minutes, not "a bit").
7. Make wins visible.
8. Matter-of-fact errors.
9. Cap lists at 5 items.
10. No preamble. No recap. No closers.

## Install (local plugin)

This is a local-only Claude Code plugin — no marketplace publish needed. From this repo's directory:

```bash
claude plugin marketplace add /Users/connor/projects/claude-stop-talking-like-that
claude plugin install claude-stop-talking-like-that@claude-stop-talking-like-that
```

Restart Claude Code, then type `/claude-stop-talking-like-that` to turn the rules on for the current session. Say "stop adhd mode" to turn them back off.

### Always-on (optional)

A `SessionStart` hook loads the full ruleset at the start of every session, no `/claude-stop-talking-like-that` needed:

```bash
touch ~/.claude/.claude-stop-talking-like-that-always
```

If you use a custom Claude configuration directory, create the flag there instead:

```bash
touch "$CLAUDE_CONFIG_DIR/.claude-stop-talking-like-that-always"
```

Back to on-demand:

```bash
rm ~/.claude/.claude-stop-talking-like-that-always
```

The hook only fires when the flag file exists, so installing the plugin changes nothing by itself. "stop adhd mode" still turns it off for the current session.

### Update

Made a local edit to `SKILL.md`? Reload it with:

```bash
claude plugin marketplace update claude-stop-talking-like-that
```

### Uninstall

```bash
claude plugin uninstall claude-stop-talking-like-that
claude plugin marketplace remove claude-stop-talking-like-that
```

## Tune it

Just edit [`skills/claude-stop-talking-like-that/SKILL.md`](./skills/claude-stop-talking-like-that/SKILL.md) directly, then re-run the update command above.

## Credits

Forked from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) by Ayoub Ghriss (MIT licensed) — the original supports a dozen agent harnesses; this fork strips that down to a Claude Code-only local plugin.

## License

MIT.
