# ddev pull wp scripts

*Keep calm and pull your site.* 🧘

Open collection of DDEV pull scripts for happy local WordPress development. Pull in the latest site content to your local development enviroment for peaceful and safe testing. 

Requires at least [DDEV 1.18.2](https://github.com/drud/ddev/releases/tag/v1.18.2), Status: Work in Progress

## Scripts

- `ddev pull ssh` 👉  pull site via SSH
- `ddev pull backup` 👉  import a BackWpUp .zip-file

Screencasts: *coming soon*

## General setup

**Online generator:**

1. Use the [Online Generator](https://mandrasch.github.io/ddev-pull-wp-generator/)
1. Overwrite your local files with the generated `.ddev/config.yaml`and `.gitignore` from the Online Generator

**Manual setup:**

1. Copy `.ddev/example.config.yaml` to `.ddev/config.yaml`
1. Adjust your configuration
1. Adjust child theme folder name in `.gitignore`
and adjust your configuration or 

## Usage

## ddev pull ssh

Pull in your live WordPress site via SSH, your webspaces needs support for WP-CLI or mysqldump.

1. `ddev start` (on first start)
1. `ddev pull ssh`

You need to be able to connect to your SSH webspace via SSH key authentication (without password). On first run DDEV will ask you to run `ddev auth ssh`. 

## ddev pull backup

Create and download a BackWpUp backup-file from your live site, Import it your local DDEV project.

1. `ddev start`
1. Create backup with [BackWPup – WordPress Backup Plugin](https://wordpress.org/plugins/backwpup/) (Open Source) on your live site
1. Download BackWpUp .zip file to root of local project folder
1. Rename backup file to `backup.zip`
1. `ddev pull backup`
1. Open imported website in browser: `ddev launch`

## Technical Documentation

Pull scripts are import steps for database and files which are stored as .yaml-files in `.ddev/providers`. They can be executed via `ddev pull`. See [DDEV pull (providers)](https://ddev.readthedocs.io/en/stable/users/providers/provider-introduction/) documentation for more insights.

### Reset / delete

- `git clean -fdx -e .ddev`
    - removes all synced (untracked) files and directories, but without deleting the DDEV folder
- `git clean -fdx`
    - removes all untracked files and directories
    - if .ddev/config.yaml is untracked, it will be removed as well
    - you need to run 'ddev start' again afterwards
- `ddev delete -O`
    - deletes DDEV project with database and containers (git-tracked files will be kept)