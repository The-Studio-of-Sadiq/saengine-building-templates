# saengine-building-templates

Building templates for [SAEngine](https://github.com/The-Studio-of-Sadiq/SAEngine): ordinary
buildings to start a project from, installable from the app's Packages page once it exists
(marketplace round M3) and applied by the New Building wizard or *New Project from Template…*
(M4). Each top-level folder is one package, `<id>/pack.json` with
`"kind": "buildingTemplate"`, and either:

- `spec.json`: a building specification (SAEngine's `BuildingSpec`, schema
  `building-template.schema.json`) that prefills the New Building wizard; or
- `template.civil`: an **inputs-only** SAEngine project archive (floor plan, architecture, BIM,
  MEP inputs, settings). Never results, never a soil report, never deliverables or the version
  history: the validator refuses them. A template never holds client data: no real client's
  project, no site located more precisely than its town.

| Package | What it is |
| --- | --- |
| `saengine-default-building` | The New Building wizard's starting values: Dhaka, 6 storeys, RC frame, 3 × 2 bays. |

## Adding or changing a package

1. `licence`: an SPDX id, `CC-BY-4.0` by default; `requires.packages` names the design code the
   template was made with (e.g. `{"bnbc2020": ">=1.0.0"}`).
2. A `preview.png` of at most 256 KB and 1024 px a side.
3. Raise `version` whenever a published package changes.
4. Check locally: `saengine codepack validate <folder> --kind buildingTemplate`.
5. Open a pull request; CI (defined once in
   [saengine-index](https://github.com/The-Studio-of-Sadiq/saengine-index)) checks each changed
   package.

## Publishing

A maintainer pushes a tag `packages-YYYY-MM-DD` on main; `.github/workflows/publish.yml` builds
the zips and `packages.json` and creates an immutable GitHub Release, which saengine-index lists
in its signed `index.json`. Running the workflow by hand is a dry run.
