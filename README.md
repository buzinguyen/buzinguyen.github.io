# Initialise

Run the following commands (in WSL)
- Fetch metadata
```commandline
bundle
```
- Build Jekyll
```commandline
bundle exec jekyll build
```
- Host web in localhost
```
bundle exec jekyll serve
```

# How to edit pages

Add entries to corresponding data YML file to edit pages
- Index (experience): `_data/experience.yml`
- Publications: `_data/publications.yml`
- News: `_data/news.yml`
    - currently there are labels: **feature**, **research-update**, **achievement**
- Research: create new Markdown file for each entry in `_posts/`, file name should be `YYYY-MM-DD-post-name.md`

The `img` field in YML files can store either:
- local path to image stored in `assets/img/{{page}}/{{image_name}}.{{extension}}` (`Zone.Identifier` object is automatically created for each image)
- image URL from the internet

# Other notes

- If auto-reload doesn't work, try adding `--force-polling` flag
```commandline
bundle exec jekyll serve --force-polling
```