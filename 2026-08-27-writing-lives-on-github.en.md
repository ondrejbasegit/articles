---
nazev: The writing lives on GitHub, the site comes and gets it
typ: clanek
druh: NOTE
popis: One public repository is the source. The site reads it at build time and typesets it. No admin interface, no database.
---

# The writing lives on GitHub, the site comes and gets it

One public repository is the source. The site reads it at build time and
typesets it.

## Why not a CMS

A CMS solves a problem I don't have. It would mean a database, logins, backups
and updates — a whole layer that has to keep running for a page of text to be
readable. In return I get an editing box in a browser.

A repository has three properties I value more. Its change history is free and
complete. The text opens in anything that opens a file. And when the site
breaks, the writing doesn't suffer — it lives elsewhere, in a format that
outlives whatever technology happens to be doing the typesetting.

## What's in the repository

Articles are plain Markdown files. The filename carries the slug, the language
and the date:

```
2026-08-27-writing-lives-on-github.en.md
2026-08-27-writing-lives-on-github.cs.md
```

Two files sharing a slug are the same text in two languages. They can have
completely different titles; what joins them is the part between the date and
the language suffix. When only one version exists, the site offers it in the
other language too and says above the text that the translation isn't there yet.

At the top of the file sits a header — title, kind, standfirst. The rest is the
text.

## Images

Images sit next to the writing and are referenced by a relative path:

<figure>
  <img src="images/flow.webp"
       alt="Three steps side by side: repository, build, finished page"
       width="1600" height="300" loading="lazy" />
  <figcaption>The middle step runs on every build. Between it and the finished page, nothing runs at all.</figcaption>
</figure>

The relative path has one advantage, which is the reason it works this way: the
image also shows up on GitHub itself. The article is readable in both places,
not just on the site. At build time the path is rewritten to an address the
browser can fetch.

## What happens at build time

The site asks GitHub for a file listing, downloads the files, validates the
headers and typesets static pages. If a required field is missing from a header,
the build fails — deliberately, because that beats quietly shipping a page with
a hole in it.

What comes out is just HTML. No request to GitHub ever leaves the browser.
