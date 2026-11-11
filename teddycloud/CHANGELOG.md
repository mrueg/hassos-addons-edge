# Changelog since v0.5.7
- Restart TeddyCloud instead of stopping the add-on on restart request

A restart from the web UI makes TeddyCloud exit with -2 (254), which
upstream's entrypoint answers by starting it again. The finish script
treated it as a crash and halted the container. Let S6 restart the
service instead.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Always create certs and config directories

Like upstream's entrypoint, create certs/server, certs/server_tb2,
certs/client and config on every start instead of only on a fresh
install, so /teddycloud/certs and /teddycloud/config never point to a
missing directory.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Fix migration of the old certs and config layout

The default /config/teddycloud/certs/server directory was created
before /config/certs was moved there, so mv failed with "Directory not
empty" and the add-on stopped at every start. Migrate first, replace
an existing target only when it holds no files (as left behind by an
earlier failed attempt), and otherwise keep the new path and warn.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Exclude the download cache from backups

The cache only holds files downloaded from the internet, which
TeddyCloud fetches again when needed.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Clean up nginx config

Normalize indentation and drop settings that have no effect:
proxy_read_timeout at http level is overridden by the ingress server,
and proxy_max_temp_file_size is unused with proxy buffering off.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Add shellcheck shell directive to nginx finish script

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Fix maintainer label typo and whitespace in Dockerfile

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Always create data directories, including plugins

The Dockerfile links /teddycloud/data/www/plugins to
/data/teddycloud/plugins, but that directory was never created, and the
data directories were only created when /data/teddycloud was empty, so
existing installs never got directories added in later versions.
Create all of them on every start.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Bump git, curl, ca-certificates and nginx package pins

The previous versions are no longer available in the Ubuntu archive,
which broke the build.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Drop ingress sub_filter rewrites

Since v0.7.1 the TeddyCloud web UI derives its URL prefix from the
browser location at runtime and prefixes all backend paths itself, so
rewriting proxied responses is no longer needed. Keep proxy_redirect
for the backend's / -> /web redirect.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Bump teddycloud to v0.7.1

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
