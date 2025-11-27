# Release

## Release guidelines

**tl;dr**: Majors about once per year, minors for any finished features with docs, patches for any committed bugfix.

Patch (bugfix) releases should generally be cut as soon as possible. A patch release for a single bugfix PR is totally okay.

Minor (feature) releases can be cut anytime at least one new feature is ready, but don't have to be. Minor version releases must update their major version's man pages and docs website as needed, and should each have their own "What's new?" section.

Major (breaking) version releases should be cut no more than once per year, and must include a new section of the docs website dedicated to that major version. Ideally, major releases will happen after a Ruby version loses support in February or March, to help us stay in sync with Ruby versions supported by the core team.

Breaking changes other than dropping support for old Ruby versions should be avoided whenever possible, but may be included in major releases. In general, breaking changes should include at least one major version (and one year elapsed) with a deprecation warning before the breaking change takes effect.

### User experience guidelines

The experience of using Bundler should not include surprises. If users are surprised, we did something wrong, and we should fix it. There are no user errors, only UX design failures. Warnings should always include actionable instructions to resolve them. Errors should include instructions, helpful references, or other information to help users attempt to debug.

Changing existing behavior is also surprising. If reducing user surprise will result in a backwards-incompatible change, that change should include at least one major version of deprecation warning before the breaking change is made.

## Release Process

### Permissions

You'll need the following environment variables set to release RubyGems & Bundler:

* AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY: to be able to push RubyGems zip files to s3 so that they appear at RubyGems [download page].

* GITHUB_RELEASE_PAT: A [GitHub PAT] with repo permissions, in order to push GitHub releases and to use the GitHub API for changelog generation.

[download page]: https://rubygems.org/pages/download
[GitHub PAT]: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

### Recommendations for security releases

*   Obtain CVE numbers as needed from HackerOne or Red Hat.
*   Agree on a release date with ruby-core, so patches can be backported to older Ruby versions as needed.
*   Avoid releasing security updates on Fridays, so platform services don't have to work on weekends.
*   Continue with the regular release process below.

### Branching

Bundler releases are synchronized with rubygems releases at the moment. That means that releases for both share the same stable branch, and they should generally happen together.

The current conventional naming for stable branches is `x+1.y`, where `x.y` is the version of `bundler` that will be released. This is because `rubygems-x+1.y` will be released at the same time.

For example, `rubygems-3.2.0` and `bundler-2.2.0` were both released from the `3.2` stable branch.

Once a stable branch has been cut from `master`, changes for that minor release series are only made _intentionally_, via patch releases. That is to say, changes to `master` by default _won't_ make their way into the current stable branch, and development on `master` will be targeting the next minor or major release.

There is a `bin/rake prepare_release[<target_rubygems_version>]` rake task that helps with creating a release. It takes a single argument, the _exact rubygems release_ being made (e.g.  `3.2.3` when releasing bundler `2.2.3`). This task checks out the appropriate stable branch (`3.2`, for example), grabs all merged but unreleased PRs from both bundler & rubygems from GitHub that are compatible with the target release level, and then cherry-picks those changes (and only those changes) to a new branch based off the stable branch. Then bumps the version in all version files, synchronizes both changelogs to include all backported changes and commits that change on top of the cherry-picks.

Note that this task requires all user facing pull requests to be tagged with specific labels. See [Merging a PR](../bundler/playbooks/MERGING_A_PR.md) for details.

Also note that when this task cherry-picks, it cherry-picks the merge commits using the following command:

```bash
$ git cherry-pick -m 1 MERGE_COMMIT_SHAS
```

For example, for PR [#5029](https://github.com/rubygems/bundler/pull/5029), we cherry picked commit [dd6aef9](https://github.com/rubygems/bundler/commit/dd6aef97a5f2e7173f406267256a8c319d6134ab), not [4fe9291](https://github.com/rubygems/bundler/commit/4fe92919f51e3463f0aad6fa833ab68044311f03) using:

```bash
$ git cherry-pick -m 1 dd6aef9
```

After running the task, you'll have a release branch ready to be merged into the stable branch. You'll want to open a PR from this branch into the stable branch and provided CI is green, you can go ahead, merge the PR and run release tasks as specified below from the updated stable branch.

### Automatic changelog and backport generation

PR labels and titles are used to automatically generate changelogs for patch and minor releases.

When releasing, a changelog generation script goes through all PRs that have never made it into a release, and selects only the ones with specific labels as detailed in the `.changelog.yml` and `bundler/.changelog.yml` files. Those particular PRs get backported to the stable branch and included in the release changelog.

If PRs don't have a proper label, they won't be backported to patch releases.

If you want a PR to be backported to a patch level release, but don't want to include it in the changelog, you can use the special `rubygems: skip changelog` and `bundler: skip changelog` labels. For example, this is useful when backporting a PR generates conflicts that are solved by backporting another PR with no user visible changes. You can use these special labels to also backport the other PR and not get any conflicts.

### Breaking changes

Bundler cares a lot about preserving compatibility. As a result, changes that break backwards compatibility should (whenever this is possible) include a feature release that is backwards compatible, and issue warnings for all options and behaviors that will change.

We only release major breaking changes when incrementing the _major_ version of Bundler and RubyGems. However, experience shows that almost every single part of Bundler and RubyGems is depended on by someone in ways hard to anticipate. So if we were strict about breaking changes we'd need to hold on from making progress a lot, or continuously increment the major version, emptying "really major" versions from their meaning. Because of this, we also may release "small" breaking changes in minor releases. "Small" here means that we expect them to affect only very few users in rare cases.

### Steps for patch releases

*   Confirm all PRs that you want backported are properly tagged with `rubygems: <type>` or `bundler: <type>` labels at GitHub.
*   Run `bin/rake prepare_release[<target_rubygems_version>]`. This will create a PR to the stable branch with the backports included in the release, and proper changelogs and version bumps. It will also create a PR to merge release changelogs into master.
*   Once CI passes, merge the release PR, switch to the stable branch and pull the PR just merged.
*   Release `bundler` with `bin/rake bundler:release`.
*   Release `rubygems` with `bin/rake release`.

### Steps for minor and major releases

*   Confirm all PRs that you want listed in changelogs are properly tagged with `rubygems: <type>` or `bundler: <type>` labels at GitHub.
*   Run `bin/rake prepare_release[<target_rubygems_version>]`. This will create a new stable branch off the master branch, and create a PR to it with the proper version bumps and changelogs. It will also create a PR to merge release changelogs into master.
*   Replace the stable branch in the workflows with the new stable branch, and push that change to the release PR.
*   Replace version numbers with the next ".dev" version, and push that change to the master PR.
*   Once CI passes, merge the release PR, switch to  the stable branch and pull the PR just merged.
*   Release `bundler` with `bin/rake bundler:release`.
*   Release `rubygems` with `bin/rake release`.
