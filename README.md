# Unofficial mirror of Deno Docs

This is an unofficial mirror of Deno Docs(docs.deno.com). It is automatically built from [denoland/docs](https://github.com/denoland/docs) and hosted on Github Page.

[![Deploy](https://github.com/FBIKdot/deno-docs/actions/workflows/deploy.yml/badge.svg)](https://github.com/FBIKdot/deno-docs/actions/workflows/deploy.yml)

<https://deno.0.9.b.f.0.7.4.0.1.0.0.2.ip6.arpa>

## The solution to support Github Page

The official Deno docs seem to use a custom middleware for URL handling. This implementation provides similar functionality through build-time processing:

```yaml
- name: Replace domain
  run: find _site -type f -exec sed -i 's|docs\.deno\.com|fbikdot.github.io/deno-docs|g' {} +

- name: support Github Page - handle html with no .html
  run: |
    find "./_site/api" -type f ! \( -name "*.html" -o -name "*.png" \) | while read -r file; do
      newfile="${file}.html"
      mv -v "$file" "$newfile"
    done

 - name: support Github Page - Redirect file
  run: |
    echo "<meta name=\"color-scheme\" content=\"light dark\"><meta http-equiv=\"refresh\" content=\"0; url=./runtime/\">" > ./_site/index.html
    echo "<meta name=\"color-scheme\" content=\"light dark\"><meta http-equiv=\"refresh\" content=\"0; url=./deno/~/Deno\">" > ./_site/api/index.html
    mv ./_site/404/index.html ./_site/404.html

```
