# DDEV pull wp scripts

🧘&nbsp; *Keep calm and pull your site.* 🧘

Open collection of DDEV pull scripts for happy local WordPress development: Pull in the latest site content to your local dev sever. Test, develop and design in peace without breaking your live site. These scripts require at least [DDEV 1.18.2](https://github.com/drud/ddev/releases/tag/v1.18.2).

Status: *Work in Progress, please use with caution.*

## Scripts

- ⚡️&nbsp; `ddev pull ssh` - *pull a site with just one command*<br>
- 💾 &nbsp; `ddev pull backup` - *download and import a BackWpUp .zip-file*

## Helpful resources

- Screencasts: [ddev pull ssh](https://www.youtube.com/watch?v=lEGL65H-hts)
- Online config generator: [DDEV pull wp generator](https://mandrasch.github.io/ddev-pull-wp-generator/), [GitHub](https://github.com/mandrasch/ddev-pull-wp-generator/)
- [DDEV discord community](https://discord.gg/kDvSFBSZfs)

## Usage

## ⚡️&nbsp;  ddev pull ssh

Pull in your live WordPress site via SSH (and rsync). Your webspace needs support for WP-CLI or mysqldump, you need to be able to connect to your SSH webspace via SSH key authentication (without password).

**First time project setup**

1. Copy `.ddev/example.config.yaml` to `.ddev/config.yaml`
   (You can as well use the [Online Generator](https://mandrasch.github.io/ddev-pull-wp-generator/))
1. Configure SSH host, user and WordPress path on server in `.ddev/config.yaml`
1. Run `ddev start`
1. Run `ddev auth ssh`
1. Test ssh connection with `ddev ssh production'` (custom command), use `exit` to leave ssh terminal afterwards. Make sure there is no message `No such file or directory` and use `pwd` to check, that you're in the correct directory.

Nice! You ready to pull!

**(Optional) Child theme setup**

*Skip these steps, if you don't have a child theme on your live site which you want to manage via git*

1. Configure Child theme folder name in `.ddev/config.yaml` 
1. Run `ddev restart`
1. Adjust child theme folder name in `.gitignore`
1. Download your current child theme to the repository (use the custom command `ddev ssh-production-download-child-theme` or use [plugin](https://de.wordpress.org/plugins/download-plugins-dashboard/), now you can git manage it. 
1. For pushing it see [WPPusher - Github Install Theme documentation](https://docs.wppusher.com/article/17-setting-up-a-plugin-or-theme-on-github)

**Pull in your latest site content**

1. Run `ddev pull ssh`

That's it, run `ddev launch` to open your site in the web browser. If you experience issues, see [Troubleshooting](#troubleshooting).

Source code: [.ddev/providers/ssh.yaml](https://github.com/mandrasch/ddev-pull-wp-scripts/blob/main/.ddev/providers/ssh.yaml)

If you want to clean and delete all pulled filles, you can use `git clean -fdx -e .ddev`. 




## 💾 &nbsp;ddev pull backup

Create and (manually) download a BackWpUp backup-file from your live site, import it to your local DDEV project. No SSH required, just download your backup file and import it as .zip-file.

**First time project setup**

1. Copy `.ddev/example.config.yaml` to `.ddev/config.yaml`
1. Configure Child theme folder name in `.ddev/config.yaml` (optional)
3. Adjust child theme folder name in `.gitignore` (optional)
4. Run `ddev start` and `ddev auth ssh`

**Import a backup:**

1. Create a backup with [BackWPup – WordPress Backup Plugin](https://wordpress.org/plugins/backwpup/) (Open Source) on your live site
1. Download BackWpUp .zip file to root of local project folder
1. Rename backup file to `backup.zip`
1. `ddev pull backup`
1. Open imported website in browser: `ddev launch`

Source code: [.ddev/providers/backup.yaml](https://github.com/mandrasch/ddev-pull-wp-scripts/blob/main/.ddev/providers/backup.yaml)

## Child theme deployment

You can optionally manage a child theme via git and deploy it with a tool like [WPPusher](https://wppusher.com/) (no git on server required). This repository already contains an example child theme. 

## Technical Documentation

Pull scripts are import steps for database and files which are stored as .yaml-files in `.ddev/providers`. They can be executed via `ddev pull`. See [DDEV pull (providers)](https://ddev.readthedocs.io/en/stable/users/providers/provider-introduction/) documentation for more insights.

 Design, test  and develop sites in local isolated [DDEV](https://ddev.readthedocs.io/en/stable/) project environments without breaking the live site.

### Reset / delete

- `git clean -fdx -e .ddev`
    - removes all untracked files and directories, but without deleting the DDEV folder
- `git clean -fdx`
    - removes all untracked files and directories
    - if .ddev/config.yaml is untracked, it will be removed as well
    - you need to run 'ddev start' again afterwards
- `ddev delete -O`
    - deletes DDEV project with database and containers (git-tracked files will be kept)

## Troubleshooting

### DDEV version correct?

Please check with `ddev -v` that you are using [DDEV 1.18.2](https://github.com/drud/ddev/releases/tag/v1.18.2) or newer.

### ERR_TOO_MANY_REDIRECTS (apache)

If .htaccess has a https-only rule with something like 'RewriteCond %{HTTPS} !=on', it will result in 'ERR_TOO_MANY_REDIRECTS'. Just remove these rules from .htaccess. https://twitter.com/m_andrasch/status/1481290725694349316

## Acknowledgements

Thanks to 
- DDEV maintainer [@randyfay](https://github.com/rfay) for helpful advice
- [@dahaupt](https://github.com/dahaupt) for [advice on db sync](https://github.com/drud/ddev/discussions/2940#discussioncomment-1665163),
- all people in the WordPress & [DDEV community](https://discord.gg/kDvSFBSZfs) for sharing their knowledge online
- my colleagues at [gugler* MarkenSinn](https://www.gugler.at/markensinn)

## License

My code is released as [CC0 Public Domain](https://tldrlegal.com/license/creative-commons-cc0-1.0-universal), feel free to use it with or without attribution.
