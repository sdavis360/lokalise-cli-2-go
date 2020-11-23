# Lokalise CLI v2

## Getting started
Lokalise CLI v2 allows you to manipulate any object or data in your [Lokalise](https://lokalise.com) workspace, which includes files, projects, keys, translations, comments, contributors, teams and more. 

## Whats new in v2?
This version of CLI tool has been completely rebuilt from scratch and is **not compatible** with the v1 CLI command syntax. Instead of being just an upload/download tool this release supports all [Lokalise API v2](https://lokalise.com/api2docs/curl/) endpoints.

## Installation
Get the binaries for your platform, unarchive and put into any executable folder. All set! 

### MacOS
Install using Homebrew:
```console
brew tap lokalise/cli-2
brew install lokalise2
```
Direct download:

- [lokalise2_darwin_x86_64.tar.gz](https://github.com/lokalise/lokalise-cli-2-go/releases/latest/download/lokalise2_darwin_x86_64.tar.gz)


### Linux
Get the binaries (including for Raspberry Pi) using our installer script:
```console
curl -sfL https://raw.githubusercontent.com/lokalise/lokalise-cli-2-go/master/install.sh | sh
```
Direct download:

- [lokalise2_linux_i386.tar.gz](https://github.com/lokalise/lokalise-cli-2-go/releases/latest/download/lokalise2_linux_i386.tar.gz)
- [lokalise2_linux_x86_64.tar.gz](https://github.com/lokalise/lokalise-cli-2-go/releases/latest/download/lokalise2_linux_x86_64.tar.gz)

### FreeBSD
- [lokalise2_freebsd_i386.tar.gz](https://github.com/lokalise/lokalise-cli-2-go/releases/latest/download/lokalise2_freebsd_i386.tar.gz)
- [lokalise2_freebsd_x86_64.tar.gz](https://github.com/lokalise/lokalise-cli-2-go/releases/latest/download/lokalise2_freebsd_x86_64.tar.gz)

### Windows
Install using [`scoop`](https://scoop.sh):
```console
scoop bucket add extras
scoop install lokalise2
```
Direct download:
- [lokalise2_windows_i386.zip](https://github.com/lokalise/lokalise-cli-2-go/releases/latest/download/lokalise2_windows_i386.zip)
- [lokalise2_windows_x86_64.zip](https://github.com/lokalise/lokalise-cli-2-go/releases/latest/download/lokalise2_windows_x86_64.zip)

### Docker
See [DockerHub](https://hub.docker.com/r/lokalise/lokalise-cli-2) for more information.

## Tokens
All endpoints require the `--token` parameter. You can generate your API token in [Personal profile](https://lokalise.com/profile). Note, the token is personal and mimics your access level on team and project level. If you require a user-independent API token, create a separate user in your team (e.g. API user), set proper access rights and use this user's token.

## Passing the flags

#### Boolean
All `boolean` flags **must** be passed via the `=` sign, i.e. `--original-filenames=false`. 

#### Strings
Flags of type `strings` should be comma-delimited, i.e. `--include-tags=one,two`. 

#### JSON objects
Some flags require a JSON-encoded object passed as string, i.e. `--languages='[{"lang_iso":"en","custom_iso":"en-us"},{"lang_iso":"en_GB","custom_iso":"en-gb"}]'`. There is an [online tool](https://tools.knowledgewalls.com/jsontostring) to help you with the escaping.

## Usage
Run `lokalise2 --help` from the terminal to see the list of commands and subcommands. Run `lokalise2 command subcommand --help` to see the help page.

### Commands

* [lokalise2 branch](docs/lokalise2_branch.md)	 - Manage branches
* [lokalise2 comment](docs/lokalise2_comment.md)	 - Manage key comments
* [lokalise2 contributor](docs/lokalise2_contributor.md)	 - Manage project contributors
* [lokalise2 file](docs/lokalise2_file.md)	 - Upload and download files
* [lokalise2 key](docs/lokalise2_key.md)	 - Manage keys
* [lokalise2 language](docs/lokalise2_language.md)	 - Manage languages
* [lokalise2 order](docs/lokalise2_order.md)	 - Manage orders
* [lokalise2 payment-card](docs/lokalise2_payment-card.md)	 - Manage payment cards
* [lokalise2 project](docs/lokalise2_project.md)	 - Manage projects
* [lokalise2 queued-process](docs/lokalise2_queued-process.md)	 - Manage queued processes
* [lokalise2 screenshot](docs/lokalise2_screenshot.md)	 - Manage screenshots
* [lokalise2 snapshot](docs/lokalise2_snapshot.md)	 - Manage snapshots
* [lokalise2 task](docs/lokalise2_task.md)	 - Manage tasks
* [lokalise2 team](docs/lokalise2_team.md)	 - List teams
* [lokalise2 team-user](docs/lokalise2_team-user.md)	 - Manage team users
* [lokalise2 team-user-group](docs/lokalise2_team-user-group.md)	 - Manage team user groups
* [lokalise2 translation](docs/lokalise2_translation.md)	 - Manage translations
* [lokalise2 translation-provider](docs/lokalise2_translation-provider.md)	 - List translation providers
* [lokalise2 translation-status](docs/lokalise2_translation-status.md)	 - Manage custom translation statuses
* [lokalise2 webhook](docs/lokalise2_webhook.md)	 - Manage webhooks

### Examples

#### Download files from Lokalise
```bash
lokalise2 \
    --token <token> \
    --project-id <project_id> \
    file download \
    --format json \
    --unzip-to ./locales
```

#### Upload a file to Lokalise
```bash
lokalise2 \
    --token <token> \
    --project-id <project_id> \
    file upload \
    --file /tmp/en.json \
    --lang-iso en
```

## Branches
If you are using project branching feature in Lokalise, simply add branch name separated by semicolon to the project ID in any command to access the branch, i.e. `3002780358964f9bab5a92.87762498:feature/new-release`.

## Config file
Optionally, you may rename included `config-example.yml` to `config.yml` and set various CLI tool parameters like token or timeouts. You can specify a config file location using `--config` parameter.

## Changes
**2.6.1 (October 28, 2020)**
          
- Fixed file path detection for file upload action

**2.6.0 (August 5, 2020)**
          
- Added BDS-Clause-3 license

**2.5.2 (July 28, 2020)**
          
- Added `--skip-detect-lang-iso` flag for file upload action

**2.5.1 (May 28, 2020)**

- Fix flag naming typo for file upload
  - Changed `--pool` to `--poll`
  - Changed `--pool-timeout` to `--poll` 
  
**2.5.0 (May 28, 2020)**

- Added queued process [commands](docs/lokalise2_queued-process.md)
- Changed file upload to use queued processing
  - Added `--pool` flag to obtain the upload result
  - Added `--pool-timeout` flag to configure the upload pooling maximum duration
  - Changed `--convert-placeholders` default value to `true`

**2.3.1 (April 30, 2020)**

Added `--custom-translation-status-ids` flag for file upload action, along with `--custom-translation-status-inserted-keys`, `--custom-translation-status-skipped-keys` and `--custom-translation-status-updated-keys` flags

**2.3.0 (February 26, 2020)**

Added `--hidden-from-contributors` flag for file upload action

**2.2.3 (February 7, 2020)**

Added better description for boolean flags

**2.2.2 (January 27, 2020)**

Changed upper case in archive names. Removed README.md from binary archives

**2.2.1 (January 17, 2020)**

Fixes:
* `--project-id` hasn't been processed correctly

**2.2.0 (January 16, 2020)**

Added possibility to specify a configuration file with a --config flag 

**2.1.0 (November 25, 2019)**

Updated go-lokalise-api library version, bug fixes, switched binary building to goreleaser

**2.03 (October 22, 2019)**

Endpoint parameter fixes.

**2.00 (October 15, 2019)**

Initial release. 

