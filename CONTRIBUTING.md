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
