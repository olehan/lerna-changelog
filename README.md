lerna-changelog-gitlab
==============================================================================

> Forked from [`lerna-changelog`](https://github.com/lerna/lerna-changelog)
>
> Everything is the name, expect it's integrated with Gitlab!

[![Latest NPM release][npm-badge]][npm-badge-url]

[npm-badge]: https://img.shields.io/npm/v/lerna-changelog-gitlab.svg
[npm-badge-url]: https://www.npmjs.com/package/lerna-changelog-gitlab

**Gitlab** PR-based changelog generator with monorepo support


Install
------------------------------------------------------------------------------

Install with `yarn`:

```bash
yarn add lerna-changelog-gitlab --dev
# or globally
yarn global add lerna-changelog-gitlab
```

We're using `yarn` but you can use `npm` if you like:

```bash
npm install --save-dev lerna-changelog-gitlab
# or globally
npm install --global lerna-changelog-gitlab
```


Usage
------------------------------------------------------------------------------

```bash
$ lerna-changelog-gitlab
```

```md
## Unreleased (2018-05-24)

#### :bug: Bug Fix
* [#198](https://github.com/my-org/my-repo/pull/198) Avoid an infinite loop ([@helpful-hacker](https://github.com/helpful-hacker))

#### :house: Internal
* [#183](https://github.com/my-org/my-repo/pull/183) Standardize error messages ([@careful-coder](https://github.com/careful-coder))

#### Commiters: 2
- Helpful Hacker ([@helpful-hacker](https://github.com/helpful-hacker))
- [@careful-coder](https://github.com/careful-coder)
```

By default `lerna-changelog-gitlab` will show all pull requests that have been merged
since the latest tagged commit in the repository. That is however only true for
pull requests with certain labels applied. The labels that are supported by
default are:

- `breaking` (:boom: Breaking Change)
- `enhancement` (:rocket: Enhancement)
- `bug` (:bug: Bug Fix)
- `documentation` (:memo: Documentation)
- `internal` (:house: Internal)

You can also use the `--from` and `--to` options to view a different
range of pull requests:

```bash
lerna-changelog-gitlab --from=v1.0.0 --to=v2.0.0
```

### Monorepo support

If you have a packages folder and your projects in subfolders of that folder `lerna-changelog-gitlab` will detect it and include the package names in the changelog for the relevant changes.

### GitHub Token

Since `lerna-changelog-gitlab` interacts with the GitLab API you may run into rate
limiting issues which can be resolved by supplying a "personal access token":

```
export AUTH_TOKEN="..."
```

You'll need a [personal access token](https://github.com/settings/tokens)
for the GitLab API with the `read_repository` scope for your private repositories.


Configuration
------------------------------------------------------------------------------

You can configure `lerna-changelog-gitlab` in various ways. The easiest way is by
adding a `changelog` key to the `package.json` file of your project:

```json5
{
  // ...
  "changelog": {
    "labels": {
      "feature": "New Feature",
      "bug": "Bug Fix"
    }
  }
}
```

The supported options are:

- `repo`: Your "org/repo" on GitHub
  (automatically inferred from the `package.json` file)

- `nextVersion`: Title for unreleased commits
  (e.g. `Unreleased`)

- `labels`: GitHub PR labels mapped to changelog section headers

- `ignoreCommitters`: List of committers to ignore (exact or partial match).
  Useful for example to ignore commits from bots.

- `cacheDir`: Path to a GitHub API response cache to avoid throttling
  (e.g. `.changelog`)


License
------------------------------------------------------------------------------

`lerna-changelog` is released under the [MIT License](LICENSE).
