# Casey Henderson — security notes

Jekyll site for security writeups and lab notes. GitHub Pages builds it from the `main` branch and publishes it at <https://loamranger1313.github.io>.

Adding a post is a Markdown file in `_posts`, then a commit and a push.

## Add a post

1. Copy `_drafts/TEMPLATE.md` to `_posts/YYYY-MM-DD-short-title.md`.
2. Set `title`, `date`, `categories`, `tags`, and `description` in the front matter.
3. Use one category. `writeups` lists the post on the Writeups page. `labs` lists it on the Labs page. Any other category is listed on the Categories page.
4. Tags are free-form. `Linux` and `linux` are different tags, so pick one case and keep it.
5. Write the note in Markdown. The opening paragraph is the RSS excerpt. `description` is the sentence on the home page and in link previews.
6. Commit and push to `main`.

Files in `_drafts/` stay unpublished. `bundle exec jekyll serve --drafts` includes them in a local preview.

Images go in `assets/images/`. Link one like this:

```markdown
![Alt text]({{ '/assets/images/example.png' | relative_url }})
```

Put commands in a `bash` fence and output in a `text` fence. The language name is lowercase (`bash`, `text`, `yaml`, `python`).

```bash
nmap -sV -p 22,80 10.10.10.10
```

```text
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1
```

## Preview locally on Kali

Install Ruby and the build tools once:

```bash
sudo apt update
sudo apt install -y ruby-full build-essential zlib1g-dev
```

Install gems into your home directory:

```bash
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
gem install bundler
```

From this repository:

```bash
bundle install
bundle exec jekyll serve
```

Open <http://127.0.0.1:4000>. The `Gemfile` installs the `github-pages` gem (currently 232, Jekyll 3.10), which is the set Pages uses. The first `bundle install` compiles a few native gems and takes a minute.

Stop the server with Ctrl-C.

## Publishing

Push to `main`. Pages builds the site with its own Jekyll. It does not run this `Gemfile`.

In the repository: **Settings → Pages → Build and deployment**.

- Source: **Deploy from a branch**
- Branch: **main**
- Folder: **/ (root)**

No GitHub Actions workflow is required. Leave the source on "Deploy from a branch". A workflow build would ignore this Jekyll setup unless the workflow ran Jekyll itself.

The first build after Pages is enabled takes about a minute. The site is then at <https://loamranger1313.github.io>, and the feed is at <https://loamranger1313.github.io/feed.xml>.

The feed is Atom, which feed readers subscribe to as the RSS URL.

## Front matter

```yaml
---
layout: post
title: "Short specific title"
date: 2026-11-20
categories: [writeups]   # or [labs]
tags: [linux, enumeration]
description: "One sentence for the listing and the meta description."
---
```

`date` is `YYYY-MM-DD`. The site timezone is UTC, so that date displays as the day you wrote.

## Where things live

| Path | What it is |
| --- | --- |
| `_posts/` | Published notes |
| `_drafts/TEMPLATE.md` | Copy this for a new note |
| `about.md` | About page |
| `_includes/header.html` | The nav links |
| `_config.yml` | Site title, description, URL, plugins |
| `assets/css/style.scss` | Theme. Pages compiles it with Ruby Sass 3.7 |
| `assets/images/` | Images you add |

Plugins in `_config.yml` are on the GitHub Pages allowlist: `jekyll-feed`, `jekyll-seo-tag`, `jekyll-sitemap`, and `jekyll-paginate`. A plugin outside that list fails the native Pages build.
