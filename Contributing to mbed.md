# Contribution Guidelines

## Code Style

We want to keep a consistent code style in all mbed OS code, and thus we require
that contributions match our code style, which is documented
[here](https://developer.mbed.org/teams/SDK-Development/wiki/mbed-sdk-coding-style).

## Contributing Code

- Before contributing an enhancement (new feature, new port etc) please start by [discussing it on the forums](http://forums.mbed.com/c/mbed-os) to avoid duplication of work - as we or others might work on a related feature already. This will help streamline your pull request for getting it merged quickly.
- Please create seperate patches for functional patches and form patches. Form patches are effectively just whitespace changes. As part of our security review of incoming patches we run whitespace-unaware diff that ignores tabs, spaces, newlines etc. The resulting diff of a form patch must be zero differnce to the master when ignoring whitespaces and linefeeds.
- Patch contributions can be only accepted through github by creating pull request from forked versions of our repositories. This allows us to review the contributions in a user friendly and reliable way under public scrutinity.

## Contributor License Agreement

