# example-gadget

An example HTPL gadget — a template you can copy to build your own gadget.
It is a real, working gadget with three tiny functions (`shout`, `wrap`,
`repeat_text`), kept deliberately small so the shape of a gadget is what
you see, not the logic.

## What a gadget is

A gadget is an HTPL package — the unit `htpl pm` installs. Every gadget
repo has two required files:

| File | Role |
| --- | --- |
| `htpl.json` | **META** — name, version, description, and `main`. |
| `gadget.htpl` | **ENTRY** — the code, named by `main` in `htpl.json`. |

No `htpl.json`, or no file at the `main` path, means not a gadget — the
installer and the registry both refuse it.

This repo also carries `LICENSE` (MIT), this `README.md`, and
`example-gadget.test.htpl` (tests for the three functions).

## Copy this template for your own gadget

1. Copy this repo (GitHub's "Use this template" flow, or clone and
   re-point the remote).
2. Rename the gadget in `htpl.json` — change `name` (and `description`).
   Keep `main` pointing at your entry file.
3. Replace the functions in `gadget.htpl` with yours. Keep the header
   comment style: name each public function, its parameters, and what
   it returns.
4. Update `example-gadget.test.htpl` (rename it to match your gadget)
   so every function has assertions.
5. Run `htpl test` from the repo root — all assertions must pass in
   both runtimes. The template's own tests pass with the TS and Rust
   CLIs.
6. Commit and tag the version: `git tag v0.1.0` (a version is a git
   tag `vX.Y.Z`).

## Use it in a program

Install from GitHub, bypassing the registry:

```sh
htpl pm install github:HTPLorg/example-gadget@v0.1.0
```

Then import it by path:

```html
<htpl>
  <import src="gadgets/example-gadget/gadget.htpl" />
  <print value="shout('hello')" />
  <print value="wrap('b', 'bold')" />
</htpl>
```

## Publish it to the registry

The registry is static: gadget code lives on GitHub, and the registry
is an index pointing at it. To publish your gadget:

1. Make sure the repo is **public** — the registry only accepts public
   repos (its installs download tarballs anonymously).
2. Run `htpl pm publish` in the repo. It validates `htpl.json` and the
   entry file, checks the `v<version>` tag exists, and prints the
   dashboard registration URL with the exact values to enter. It posts
   nothing itself.
3. Register at <https://app.registry.htpl.hvcrealm.com>. The dashboard
   verifies you own the GitHub repo and claims the name
   first-come, first-served.
4. New registrations appear in the registry within 4 hours, when the
   batch sync writes the index. The registry itself lives at
   <https://registry.htpl.hvcrealm.com>.

## Links

- HTPL: <https://htpl.hvcrealm.com>
- Registry: <https://registry.htpl.hvcrealm.com>
- Dashboard: <https://app.registry.htpl.hvcrealm.com>

## License

MIT — see `LICENSE`.
