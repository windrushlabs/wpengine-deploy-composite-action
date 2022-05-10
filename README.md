# wpengine-deploy-composite-action

This GitHub Action deploys themes to WordPress servers hosted on WP Engine.

## Inputs used

You’ll need to Read The Fine Source for this one. There are quite a few of them. Most are required.

## Recommendations

### `source-path` and `remote-path`

Because both `source-path` and `remote-path` are passed to `rsync`, it may be helpful to understand its rules for trailing slashes on paths. From the [USAGE section of the `rsync` manpage][usage]:

> A trailing slash on the source changes this behavior to avoid creating an additional directory level at the destination. You can think of a trailing / on a source as meaning “copy the contents of this directory” as opposed to “copy the directory by name”, but in both cases the attributes of the containing directory are transferred to the containing directory on the destination. In other words, each of the following commands copies the files in the same way, including their setting of the attributes of /dest/foo:
>
> ```sh
> rsync -av /src/foo /dest
> rsync -av /src/foo/ /dest/foo
> ```

### rsync flags

You will want a file named `.deployignore` in the root of the source directory (specified in `source-path`).

It is expected that the `.deployignore` file is formatted as [an rsync(1) filter-rules file][filter-rules]. This file will be passed to rsync via its [`--exclude-from` parameter][exclude-from].

While the `.deployignore` file can be empty, you will want to add `node_modules` to it as an exclusion (`-`) if you ever plan on using Node-based anything in the repository:

```rsync-filter-rules
- node_modules
```

### Debugging

If you’re having trouble getting uploads to go into the right place, there are a couple rsync flags that may be handy to diagnose problems:

- [`--itemize-changes`][itemize-changes] (have a look at the manpage to understand its terse output)
- [`--dry-run`][dry-run]: computes changes, but doesn’t actually upload anything

## Actions, etc. documentation

- <https://github.com/elstudio/actions-js-build>
- <https://github.com/wpengine/github-action-wpe-site-deploy>
- <https://github.com/jakejarvis/cloudflare-purge-action>
- <https://download.samba.org/pub/rsync/rsync.1>:
  - <https://download.samba.org/pub/rsync/rsync.1#opt--exclude-from>
  - <https://download.samba.org/pub/rsync/rsync.1#FILTER_RULES>

[usage]: https://download.samba.org/pub/rsync/rsync.1#USAGE
[filter-rules]: https://download.samba.org/pub/rsync/rsync.1#FILTER_RULES
[exclude-from]: https://download.samba.org/pub/rsync/rsync.1#opt--exclude-from
[itemize-changes]: https://download.samba.org/pub/rsync/rsync.1#opt--itemize-changes
[dry-run]: https://download.samba.org/pub/rsync/rsync.1#opt--dry-run
