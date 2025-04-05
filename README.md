# Polymer Pantheon Quicksilver

This repository contains Pantheon Quicksilver scripts and usage instructions. It
is primarily meant to be utilized by Polymer Pantheon extensions:

- [Polymer Pantheon Drupal](https://github.com/digitalpolygon/polymer-pantheon-drupal)

This repository is intentionally structured to support the
[Terminus Quicksilver Plugin](https://github.com/pantheon-systems/terminus-quicksilver-plugin).

Terminology:

- Quicksilver project: Refers to a directory at the top level of this repository.
- Quicksilver script: Refers to a file in a Quicksilver project.

For example:

```bash
# Install the Terminus Quicksilver Plugin (latest dev recommended).
terminus self:plugin:install pantheon-systems/terminus-quicksilver-plugin:1.x-dev
# Install the Quicksilver configuration file to ~/.quicksilver/quicksilver.yml
# if it doesn't exist and update project pantheon.yml hooks and scripts
# as indicated in the README.md for each Quicksilver project.
polymer pantheon:quicksilver:install
```
