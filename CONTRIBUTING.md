# How to contribute

Community involvement is essential to RubyGems. We want to keep it as easy as
possible to contribute changes. There are a few guidelines that we need
contributors to follow to reduce the time it takes to get changes merged in.

## Guidelines

1.  New features should be coupled with tests.

2.  Ensure that your code blends well with ours:
    *   No trailing whitespace
    *   Match indentation (two spaces)
    *   Match coding style (run `bin/rake rubocop`)

3.  If any new files are added or existing files removed in a commit or PR,
    please update the `Manifest.txt` accordingly. This can be done by running
    `bin/rake update_manifest`

4.  Don't modify the history file or version number.

5.  If you have any questions, Feel free to join us on Slack, you can register
    by signing up at http://slack.bundler.io or file an issue here:
    http://github.com/ruby/rubygems/issues


For more information and ideas on how to contribute to RubyGems ecosystem, see
here: https://guides.rubygems.org/contributing/

## Getting Started

### Installing dependencies

    bin/rake setup

> **NOTE**: If the above fails with permission related errors, you're most
> likely using a global Ruby installation (like the one packaged by your OS),
> which sets `GEM_HOME` to a location regular users can't write to. Consider
> using a Ruby version manager like [RVM](https://github.com/rvm/rvm),
> [rbenv](https://github.com/rbenv/rbenv),
> [chruby](https://github.com/postmodern/chruby) or [asdf](https://github.com/asdf-vm/asdf-ruby). These will install Ruby to a
> location regular users can write to, so you won't run into permission issues.
> Alternatively, consider setting `GEM_HOME` environment variable to a writable
> location with something like `export GEM_HOME=/tmp/rubygems.gems` and try
> again.

### Manually trying your local changes

To run commands like `gem install` from the repo:

    ruby -Ilib exe/gem install

To run commands like `bundle install` from the repo:

    bundler/bin/bundle install

### Running Tests

To run the entire test suite you can use:

    bin/rake test

To run an individual test file located for example in `test/rubygems/test_deprecate.rb` you can use:

    ruby -Ilib:test:bundler/lib test/rubygems/test_deprecate.rb

And to run an individual test method named `test_default` within a test file, you can use:

    ruby -Ilib:test:bundler/lib test/rubygems/test_deprecate.rb -n /test_default/

### Running bundler tests

To run the entire bundler test suite in parallel (it takes a while), run the following from the `bundler/` subfolder:

    bin/parallel_rspec

There are some realworld higher level specs run in CI, but not run by `bin/parallel_rspec`. You can run those with:

    bin/rake spec:realworld

To run an individual test file location for example in `spec/install/gems/standalone_spec.rb` you can use the following from the `bundler/` subfolder:

    bin/rspec spec/install/gems/standalone_spec.rb

To test Rubygems changes in bundler, set the path to your local Rubygems copy using the `RGV` environment variable:

    RGV=.. bin/rspec spec/install/gems/standalone_spec.rb

### Checking code style

You can check compliance with our code style with

    bin/rake rubocop

Optionally you can configure git hooks with to check this before every commit with

    bin/rake git_hooks

For more information, check [SETUP.md](../bundler/development/SETUP.md) and [DEBUGGING.md](../bundler/development/DEBUGGING.md).

## Issues

RubyGems uses labels to track all issues and pull requests. In order to
provide guidance to the community this is documentation of how labels are used
in the rubygems repository.

### Contribution

These labels are made to guide contributors to issue/pull requests that they
can help with.

*   **good first issue** - The issue described here is considered a good option
    for a new contributor. We encourage new contributors though to work on
    whichever issue they find most interesting, the ones labeled here as just
    estimated to have a reasonable level of complexity for someone new to the
    code base.
*   **help wanted** - The issue has not been claimed for work, and is awaiting
    willing volunteers!


### Type

Issues might have a light green `type: *` label,  which describes the type of
the issue.

*   **bug report** - An issue describing a bug in rubygems. This would be
    something that is broken, confusing, unexpected behavior etc.
*   **feature request** - An issue describing a request for a new feature or
    enhancement.
*   **question** - An issue that is a more of a question than a call for
    specific changes in the codebase.
*   **cleanup** - An issue that proposes cleanups to the code base without
    fixing a bug or implementing a feature.
*   **major bump** - This issue  request requires a major version bump
*   **administrative** - This issue relates to administrative tasks that need
    to take place as it relates to rubygems
*   **documentation** - This issue relates to improving the documentation for
    in this repo. Note that much of the rubygems documentation is here:
    https://github.com/rubygems/guides

Pull request might have a light orange `rubygems: *` or a light blue `bundler:
*` label which describes the pull request according to the following criteria:

*   **security fix** - A pull request that fixes a security issue.
*   **breaking change** - A pull request including any change that requires a
    major version bump.
*   **major enhancement** - A pull request including a backwards compatible
    change worth a special mention in the changelog
*   **deprecation** - A pull request that introduces a deprecation.
*   **feature** - A pull request implementing a feature request.
*   **deprecation** - A pull request that implements a performance improvement.
*   **documentation** - A pull request introducing documentation improvements
    worth mentioning to end users.
*   **minor enhancements** - A pull request introducing small but user visible changes.
*   **bug fix** - A pull request that fixes a bug report.

In the case of `bundler`, these labels are set by maintainers on PRs and have
special importance because they are used to automatically build the changelog.

### Workflow / Status

The light yellow `status: *` labels that indicate the state of an  issue,
where it is in the process from being submitted to being closed.  These are
listed in rough  progression order from submitted to closed.

*   **triage** - This is an issue or pull request that needs to be properly
    labeled by a maintainer.
*   **confirmed** - This issue/pull request has been accepted as valid, but is
    not yet immediately ready for work.
*   **ready** - An issue that is available for collaboration. This issue
    should have existing discussion on the problem, and a description of how
    to go about solving it.
*   **working** - An issue that has a specific individual assigned to and
    planning to do work on it.
*   **user feedback required** - The issue/pull request is blocked pending
    more feedback from an end user
*   **blocked / backlog** - the issue/pull request is currently unable to move
    forward because of some specific reason, generally this will be a reason
    that is outside RubyGems or needs feedback from some specific individual
    or group, and it may be a while before something it is resolved.


### Closed Reason

Reasons are why an issue / pull request was closed without being worked on or
accepted. There should also be more detailed information in the comments. The
closed reason labels are maroon `closed: *`.

*   **duplicate** - This is a duplicate of an existing bug. The comments must
    reference the existing issue.
*   **abandoned** - This is an issue/pull request that has aged off, is no
    longer applicable or similar.
*   **declined** - An issue that won't be fixed/implemented or a pull request
    that is not accepted.
*   **deprecated** - An issue/pull request that no longer applies to the
    actively maintained codebase.
*   **discussion** - An issue/pull that is no longer about a concrete change,
    and is instead being used for discussion.


### Categories

These are aspects of the codebase, or what general area the issue or pull
request pertains too. Not all issues will have a category. All categorized
issues have a blue `category: *` label.

*   **gemspec** - related to the gem specification itself
*   **API** - related to the public supported rubygems API. This is the code
    API, not a network related API.
*   **command** - related to something in `Gem::Commands`
*   **install** - related to gem installations
*   **documentation** - related to updating / fixing / clarifying
    documentation or guides


### Platforms

If an issue or pull request pertains to only one platform, then it should have
an appropriate purple `platform: *` label. Current platform labels:
**windows**, **java**, **osx**, **linux**

### Git

Please sign your commits. Although not required in order for you to contribute,
it ensures that any code submitted by you wasn't altered while you were
transferring it, and proves that it was you who submitted it and not someone
else.

Please see https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work or
https://help.github.com/en/articles/signing-commits for details on how to
to generate a signature and automatically sign your commits.
# Bug triage

Triaging is the work of processing tickets that have been opened by users. Common tasks include verifying bugs, categorizing tickets, and ensuring there's enough information to reproduce the bug for anyone who wants to try to fix it.

We've created an [issue template]( https://github.com/ruby/rubygems/issues/new?labels=Bundler&template=bundler-related-issue) to walk users through the process of how to report an issue with the Bundler project. We also have a [troubleshooting guide](../TROUBLESHOOTING.md) to diagnose common problems.

Not every ticket will be a bug in Bundler's code, but open tickets usually mean that there is something we could improve to help that user. Sometimes that means writing additional documentation or making error messages clearer.

## Triaging existing issues

When you're looking at a ticket, here are the main questions to ask:

  * Can I reproduce this bug myself?
  * Are the steps to reproduce the bug clearly documented in the ticket?
  * Which versions of Bundler (2.1.x, 2.2.x, git, etc.) manifest this bug?
  * Which operating systems (macOS, Windows, Ubuntu, CentOS, etc.) manifest this bug?
  * Which rubies (MRI, JRuby, Rubinius, etc.) and which versions (3.0.1, 3.1.2, etc.) have this bug?

Strategies for triaging a ticket:
  * Be sure to ask the user to output the entirety of their `bundle env`. Sometimes users forget to post all of their `bundle env` output in the issue.
  * After seeing the output of the user's `bundle env`, try to replicate the user's problem in your current environment. Only portions of the code base is changed in each release, so there's a good chance your version of bundler might have the same bug.
  * If you're having trouble replicating their issue with your current environment, slowly try to incorporate the user's environment setup. As in, this is where you begin matching their environment. For example, try switching to the user's version of Ruby, RubyGems, RVM, et cetera, step by step.
  * Is the user running the latest version of bundler? If not, ask them to update by running `gem install bundler`. There's a chance that the newest version of bundler has already solved their problem.

If the issue still requires user information, apply the label "user feedback required". This will help identify stale issues in the future.

If you can't reproduce the issue, chances are good that the bug has been fixed already (hurrah!). That's a good time to post to the ticket explaining what you did and how it worked.

If you can reproduce an issue, you're well on your way to fixing it. :)

## Fixing your triaged bug

Everyone is welcome and encouraged to fix any open bug, improve an error message or add documentation. If you have a fix or an improvement to a ticket that you would like to contribute, we have a small guide to help:

  1. Discuss the fix on the existing issue. Coordinating with everyone else saves duplicate work and serves as a great way to get suggestions and ideas if you need any.
  2. Review the [pull request guide](../development/PULL_REQUESTS.md).
  3. Commit the code with at least one test covering your changes to a named branch in your fork.
  4. Send us a [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) from your bugfix branch.

You do not have to update [CHANGELOG](../../../bundler/CHANGELOG.md) in your PR. Our release scripts will automatically prepare it from the title of each PR.

## Duplicates!

Finally, the ticket may be a duplicate of another older ticket. If you notice a ticket is a duplicate, simply comment on the ticket noting the original ticket's number. For example, you could say “This is a duplicate of issue #42, and can be closed”.

## Stale issues

Any issue that is waiting for more information is what we could consider "stale". And the process is:

1. If the issue is not updated in a while (2-4 weeks), we usually leave a comment saying "Hey :wave:, is this still a problem for you?".
2. If they don't respond within a week or two, then we will close the ticket.
3. If they do respond and they say it's still an issue, then we'll remind we are waiting for more information.
4. If the user doesn't provide the required information after being reminded, the ticket will be closed.
# Community

Community is an important part of all we do. If you'd like to be part of the Bundler community, you can jump right in and start helping make Bundler better for everyone who uses it.

It would be tremendously helpful to have more people answering questions about Bundler (and often simply about [RubyGems](https://github.com/ruby/rubygems) or Ruby itself) in our [issue tracker](https://github.com/ruby/rubygems/issues) or on [Stack Overflow](https://stackoverflow.com/questions/tagged/bundler).

Additional documentation and explanation is always helpful, too. If you have any suggestions for the Bundler website [bundler.io](https://bundler.io), we would absolutely love it if you opened an issue or pull request on the [bundler-site](https://github.com/rubygems/bundler-site) repository.

Sharing your experiences and discoveries by writing them up is a valuable way to help others who have similar problems or experiences in the future. You can write a blog post, create an example and commit it to GitHub, take screenshots, or make videos.

Publishing examples of how Bundler is used helps everyone, and we've discovered that people already use it in ways that we never imagined when we were writing it. If you're still not sure what to write about, there are also several projects doing interesting things based on Bundler. They could probably use publicity too.

Finally, all contributors to the Bundler project must agree to the contributor [code of conduct](https://bundler.io/conduct.html). By participating in this project you agree to abide by its terms.
# How you can help: your first commits!

If you're interested in contributing to Bundler, that's awesome! We'd love your help.

If at any point you get stuck, here's how to [get in touch with the Bundler team for help](https://bundler.slack.com).

## First contribution suggestions

We track [small bugs and features](https://github.com/ruby/rubygems/issues?q=is%3Aissue+is%3Aopen+label%3Abundler+label%3A%22good+first+issue%22) so that anyone who wants to help can start with something that's not too overwhelming.

Generally, great ways to get started helping out with Bundler are:

  - using prerelease versions (run `gem install bundler --pre`)
  - [reporting bugs you encounter or suggesting new features](https://github.com/ruby/rubygems/issues/new?labels=Bundler&template=bundler-related-issue.md)
    - see the [new features documentation](../development/NEW_FEATURES.md) for more
  - adding to or editing [the Bundler documentation website](https://bundler.io) and [Bundler man pages](https://bundler.io/man/bundle.1.html)
  - [checking issues for completeness](BUG_TRIAGE.md)
  - closing issues that are not complete
  - adding a failing test for reproducible [reported bugs](https://github.com/ruby/rubygems/issues)
  - reviewing [pull requests](https://github.com/ruby/rubygems/pulls) and suggesting improvements
  - improving existing code
  - writing code (no patch is too small! fix typos or bad whitespace)
    - get started setting up your dev environment with [these instructions](../development/SETUP.md)
  - backfilling [unit tests](https://github.com/ruby/rubygems/tree/master/bundler/spec/bundler) for modules that lack coverage.

If nothing on those lists looks good, [talk to us](https://bundler.slack.com/), and we'll figure out what you can help with. We can absolutely use your help, no matter what level of programming skill you have at the moment.
# Bundler Contributor Guidelines

Thank you for your interest in making Bundler better! We welcome contributions from everyone. Dozens of contributors like you have submitted feature improvements, fixed bugs, and written new documentation. [Join the Bundler Slack community](https://slack.bundler.io/) to connect with the Bundler core team and other contributors like you.

Before submitting a contribution, read through the following guidelines:

* [Bundler Code of Conduct](https://github.com/ruby/rubygems/blob/master/CODE_OF_CONDUCT.md) (By participating in Bundler, you agree to abide by the terms laid out in the CoC.)
* [Pull Request Guidelines](../development/PULL_REQUESTS.md)

And be sure to [set up your development environment](../development/SETUP.md).

## Feature Requests

To request substantial changes to Bundler and/or Bundler documentation, please refer to the [README](https://github.com/rubygems/rfcs/blob/master/README.md) in the [RFC repository](https://github.com/rubygems/rfcs) for instructions.

## Contributing to Bundler

Here are the different ways you can start contributing to the Bundler project:

* [First contribution suggestions](HOW_YOU_CAN_HELP.md)
* [Adding new features](../development/NEW_FEATURES.md)
* [Triaging bugs](BUG_TRIAGE.md)
* [Writing documentation](../documentation/WRITING.md)
* [Community engagement](COMMUNITY.md)

## Supporting Bundler

RubyGems is managed by [Ruby Central](https://rubycentral.org), a non-profit organization that supports the Ruby community through projects like this one, as well as [RubyConf](https://rubyconf.org), [RailsConf](https://railsconf.org), and [RubyGems.org](https://rubygems.org). You can support Ruby Central by attending or [sponsoring](sponsors@rubycentral.org) a conference, or by [joining as a supporting member](https://rubycentral.org/#/portal/signup).
