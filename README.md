## piLinux.me site


#### Static site generator

```
Hugo
```


#### For theme developers:

`themes/pilinux/layouts/_default/baseof.html`  [parent]

└─── `themes/pilinux/layouts/_default/single.html`  [child of baseof]

|--------└─── `themes/pilinux/layouts/404.html`  [child of single]

`themes/pilinux/layouts/_default/list.html`  [parent]

└─── `themes/pilinux/layouts/index.html`  [blocks are inherited from list]


#### For content editors:

- Create a new article `hugo new topic-name/article-title.md`
- Newly created `categories` and/or `topics` must be included manually in
`data/siteMenu.yml` file
- `siteMenu.yml` structure

```
menu:  
#  - title: Category name
#    icon: Font Awesome icon name
#    sub:
#      - title: Topic 1 name
#      - title: Topic 2 name
```

- Images used in an article should be placed in the same directory of that article
- Images used for SEO must be stored at
`https://github.com/piLinuxME/piLinux.me/blob/master/static/img.cdn/{topic-name}/{article-title}/`
location
- All `frontmatter` information must be up-to-date

---


#### License

Content available under a Creative Commons license
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0) unless otherwise
specified.
