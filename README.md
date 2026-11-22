# sf-eca-registry

The official registry of External Client App templates for the `sf eca` plugin
(`@composable-delivery/sf-cli-plugin-eca`).

## Layout

```
templates/<login>/.publisher.yaml     the GitHub account that publishes the folder
templates/<login>/<id>/template.yaml  a template
templates/<login>/<id>/tests/<test>/  parameter values in; exact plan and metadata out
templates/<login>/<id>/README.md      what the template does and what a person is asked to approve
maintainers.yaml                      numeric GitHub user ids of the maintainers
registry.yaml                         name, description and the pinned kit commit
```

The publisher of a template is the account of its folder; a template file never
names one. A folder's `.publisher.yaml` lists the numeric ids of the people who
may open pull requests for it, and only the registry's maintainers change it.

## Working on a template

With the plugin installed (`sf plugins install @composable-delivery/sf-cli-plugin-eca`):

```
sf eca template registry check
sf eca template registry build --write-expected --write-summaries
```

`check` validates every file. `build --write-expected` rewrites each test's
expected plan and metadata from the template as it is now, and
`--write-summaries` rewrites the generated section of each `README.md`, between
`<!-- summary:start -->` and `<!-- summary:end -->`, from the plugin's own
wording; read both diffs like any golden. The generated section comes first;
anything after the end marker is the author's own text and is kept. `build`
also writes the release bundle to `dist/`.

A template's version must be higher than before whenever its file changes.

## Where things go

- Questions, ideas and feedback: [Discussions](https://github.com/composable-delivery/sf-eca-registry/discussions).
  A maintainer converts a discussion to an issue when it becomes actionable.
- A publisher folder request, a template proposal or a report about a published template: the
  matching issue form.
- The change itself: a pull request that says `Closes #<issue>`.

The flow of a template: issue, pull request, checks, a maintainer adds the `approve-deploy` label,
the scratch deploy runs, the pull request is merged, and a maintainer tags a release.

## Release

A maintainer pushes a tag `vX.Y.Z`. The kit's release workflow builds the
bundle, attests it and publishes `@composable-delivery/sf-eca-registry-bundle`
to GitHub Packages, and attaches the same tarball to the GitHub Release, which
is where the plugin downloads it from.
