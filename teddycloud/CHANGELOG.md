# Changelog since v0.5.7
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
