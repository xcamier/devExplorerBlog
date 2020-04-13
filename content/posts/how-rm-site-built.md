---
title: "How Our Local Band Site is Built"
description: "Description of how I've built my local band site using Hugo"
authors: ["Xavier Camier"]
date: 2020-04-10T16:38:30+02:00
tags: ["Web","Tools"]
images: ["web.jpg"]
draft: false
---

### Goal: to remember how the local band site is built

Use of Type Hugo theme called [Type](https://themes.gohugo.io/type/)

### Technical details

- Modification of the CSS color in `main.css` file to replace the orange horizontal bar to the "wine" color or the band
- Copy of `l10n.toml` for the localization
- Adaptation of the `config.toml` and adding the additional menus

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
[menus]
[[menu.nav]]
    identifier = "À propos"
    name = "À propos"
    url = "/about/"
    weight = 0
[[menu.nav]]
    identifier = "Archives"
    name = "Archives"
    url = "/archives/"
    weight = 0
{{< / highlight >}}

- Modification of `post-list.html` header size to h3 
- Modification of `post-meta.html`
    - Change the title display line:
    - Use of a l10n entry. Beware, need to add the tags entry in the file	
    
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
&middot; {{ .Site.Data.l10n.tags }}:
{{< / highlight >}}
    
    - Change of the date format 

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
{{ .Date.Format "2 January 2006" }} 
{{< / highlight >}}

    - In the same like removal of the time needed to read


### Management of the galleries

Use of a secondary theme called [shortcode-gallery](https://github.com/mfg92/hugo-shortcode-gallery/)

Note: this theme must be at the same level as the main theme in the theme folder.

### Technical details

- In config.toml, add the theme

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
theme = ["hugo-type-theme", "hugo-shortcode-gallery"]
{{< / highlight >}}

- A post has to be created as a bundle: 
    - Create a folder called "test"
    - Inside the folder create an images folder that will contain the pictures to display in the gallery
    - Inside the bundle create an index.md file that will contain what you want to display

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
{{</* gallery match="images/*" sortOrder="desc" rowHeight="150" margins="5" resizeOptions="600x300 q90 Lanczos" loadJQuery="true" showExif="false" previewType="blur" embedPreview="true" */>}}
{{< / highlight >}}

Note: depending on the main theme you may have to set the loadJQuery option to true or to false. true is when the main theme doesn't use JQuery => that theme needs to load it.