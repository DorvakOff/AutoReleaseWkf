# AutoReleaseWkf

## Configuration

> **Note:** The `GITHUB_TOKEN` secret is required for this action to function. For more information,
> see [Managing GitHub Actions settings for a repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#setting-the-permissions-of-the-github_token-for-your-repository)
> in the GitHub Help documentation. and enable read/write access to the repository.

- Also, if you change the jar name in the pom.yml, you need to go to the [pipeline.yml](.github/workflows/pipeline.yml)
  file and change the name of the jar in the `JAR_NAME` env variable.

## Naming conventions

> Naming is important, it helps to understand what is going on in the branch and the commit. It also helps to automate
> the process of creating a release.

The action will parse the new commits since the last tag using
the [semantic-release](https://github.com/semantic-release/semantic-release) conventions.

semantic-release uses the commit messages to determine the type of changes in the codebase. Following formalized
conventions for commit messages, semantic-release automatically determines the
next [semantic version](https://semver.org) number.

By default semantic-release
uses [Angular Commit Message Conventions](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines).

Here is an example of the release type that will be done based on a commit messages:

<table>
<tr>
<td> Commit message </td> <td> Release type </td>
</tr>
<tr>
<td>

```
fix(pencil): stop graphite breaking when too much pressure applied
```

</td>
<td>Patch Release</td>
</tr>
<tr>
<td>

```
feat(pencil): add 'graphiteWidth' option
```

</td>
<td>Minor Release</td>
</tr>
<tr>
<td>

```
perf(pencil): remove graphiteWidth option

BREAKING CHANGE: The graphiteWidth option has been removed.
The default graphite width of 10mm is always used for performance reasons.
```

</td>
<td>Major Release</td>
</tr>
</table>

If no commit message contains any information, then **default_bump** will be used.

## Output based on the commit messages

> Version: major.minor.patch
> 
> Changing major version will **reset minor and patch** to 0
> 
> Changing minor version will **reset patch** to 0

## Credits

- [mathieudutour/github-tag-action@v6.1](https://github.com/mathieudutour/github-tag-action)
- [ncipollo/release-action@v1](https://github.com/ncipollo/release-action)