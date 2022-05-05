# wpengine-deploy-composite-action

This GitHub Action deploys themes to WordPress servers hosted on WP Engine.

## Inputs used

You’ll need to Read The Fine Source for this one. There are quite a few of them. Most are required.

## Requirements

Unless you override the default for `rsync-flags`, you’ll need a `.deployignore` file in in the directory you specify with `source-path`. It will be passed to rsync’s `--exclude-from` parameter.

The `.deployignore` file can be empty.

## Actions, etc. documentation

- <https://github.com/elstudio/actions-js-build>
- <https://github.com/wpengine/github-action-wpe-site-deploy>
- <https://github.com/jakejarvis/cloudflare-purge-action>
- <https://download.samba.org/pub/rsync/rsync.1>:
  - <https://download.samba.org/pub/rsync/rsync.1#opt--exclude-from>
  - <https://download.samba.org/pub/rsync/rsync.1#FILTER_RULES>
