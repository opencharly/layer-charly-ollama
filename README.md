# charly-ollama

The `charly-ollama` family — the owning skill for the Ollama LLM-server layer.

The `charly-ollama` candy is a **concept candy**: it ships no install content and
owns the `ollama` family's `skill:` entity whose name has no namesake candy — the
`ollama-layer` skill. The image and CLI skills of the same family are owned by
their own repos:

- `ollama-layer` (owned here) — the Ollama LLM server layer: port 11434, the
  `models` volume, the `OLLAMA_HOST` / `OLLAMA_MODELS` environment, the tarball
  vs packaged install, and the opt-in GPU backends.
- `ollama` — the Ollama image (`opencharly/box-ollama`).
- `ollama-cli` — the compiled-in `charly ollama` management CLI
  (`opencharly/plugin-ollama`).

`candy/plugin-marketplace` regenerates the standalone
[opencharly/marketplace](https://github.com/opencharly/marketplace) corpus from
these entities, so the skill is authored here and projected there.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `charly-ollama` (concept candy) |
| Install content | none — a `true` no-op `plan:` |
| Owns | 1 `skill:` entity: `ollama-layer` |
| Projected to | `marketplace/ollama/skills/` |
| Service / port | none (the `ollama-layer` skill documents port 11434) |

## How to use it

This repo is consumed as a **skill source**, not as an image layer. Edit the
`skill:` entity in `charly.yml`; the marketplace regeneration projects it into
the `/charly-ollama:ollama-layer` page. To reference the repo directly, compose
it in a box. A box is a `candy:` node carrying the box's `base:` image and a
nested `candy:` list of layer refs (the nested `candy:` is the composition list;
the outer `candy:` is the box body):

```yaml
my-box:
  candy:                  # the box body (an IMAGE is a `candy:` node carrying `base:`)
    base: fedora          # the box's base image
    candy:                # the box's composition list
      - '@github.com/opencharly/layer-charly-ollama:v2026.239.1603'
```

The Ollama service itself is installed by the `ollama` image candy, not by this
concept candy — this repo only carries the projected skill.

## Layout

- `charly.yml` — the `charly-ollama:` concept candy entity plus the
  `ollama-layer-skill:` entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-ollama:ollama-layer`
- Image / CLI skills: `/charly-ollama:ollama`, `/charly-ollama:ollama-cli`
- Authoring reference: `/charly-image:layer`
- [`opencharly/marketplace`](https://github.com/opencharly/marketplace) — the projected corpus
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
