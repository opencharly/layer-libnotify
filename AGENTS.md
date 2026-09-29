# AGENTS.md — layer-libnotify

Standalone candy repo for the `libnotify` layer — the `notify-send` desktop
notification CLI. The candy lives in `charly.yml` at the repo root: the
`require:` on `pod-dbus`, the `check:` assertions, and the embedded `skill:`
entity projected into the marketplace corpus as `/charly-selkies:libnotify`.

Canonical files:

- `charly.yml` — the `libnotify:` candy entity and the `libnotify-skill:` skill
  entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:libnotify` — the owning skill. The `notify-send` CLI, its
  package, and when to use it versus the `dbus: notify` verb. Load before editing
  or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, and service declarations). Load before editing any entity field or
  plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence; they must stay
  valid on every distro arm they run on. Scope a distro-specific check in the
  command itself — the check runner does not honour runner-level
  `exclude-distro` fields.
- The package is declared for `fedora` only; do not assume a `check:` runs on a
  distro arm that has no package section.

## Modify this repo

- Edit the `libnotify:` candy entity AND the `libnotify-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source, so a behaviour
  change not mirrored in the skill leaves the corpus stale.
- The `notify-send` binary is a convenience CLI; the `dbus: notify` check verb
  (served out-of-process by `candy/plugin-dbus`) is the check-plan path and does
  NOT depend on this candy — keep that distinction.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
