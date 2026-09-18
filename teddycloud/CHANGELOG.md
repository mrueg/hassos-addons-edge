# Changelog since v0.5.6
- Rewrite ingress sub_filter rules generically

The web UI bundle is minified, so rules keyed on minified identifiers
(it=`/api, cn=`/api/, p.tonieInfo.picture, ...) silently stopped
matching when upstream switched build tooling; most of the previous
rule set was dead against v0.7.0. Key the rules on the quote or
backtick preceding a root-absolute path instead, so they survive
re-minification, and add the CSS url(/web/...) font references that
were never rewritten.

Validated against the v0.7.0 bundle with nginx 1.24: every rewrite the
old rules produced is still produced, 96 additional root-absolute paths
(fonts, asset images, translations, /api/sse, router basename, plugin
iframes, ...) are now prefixed, and no output is otherwise modified.

Deliberately left alone: /custom_img/ (compared against and stored as
data), bare `/library${...}` (a file path) and `/plugins/<id>` router
links (the router prepends the prefixed basename itself). The JSON
response rules are kept unchanged.

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com> 
- Bump curl and nginx package pins

The pinned versions are no longer available in the Ubuntu 24.04
archive, which broke the image build.

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com> 
- Fix shellcheck warnings in s6 finish scripts

Drop the unused exit_code declaration, declare and assign
exit_code_container separately (SC2155), and remove the redundant
$ inside arithmetic expansion (SC2004).

Co-Authored-By: Claude Fable 5.1 <noreply@anthropic.com> 
- Bump teddycloud to v0.7.0 
