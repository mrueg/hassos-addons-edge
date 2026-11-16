# Changelog since v0.5.8
- Drop migration from the pre-v0.4.0 storage layout

The move of /config/certs, /config/config and /config/data into the
new layout was added in v0.4.0 (January 2025). Every install that has
started a release since then has already migrated.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
- Bump ubuntu-base to v12.0.1 (Ubuntu 26.04)

ubuntu-base v12 moves from Ubuntu 24.04 to 26.04, so update all apt
package pins to the resolute versions.

Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com> 
