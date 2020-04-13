---
title: "How This Site Is Built"
description: "Description of how I build the website using Hugo"
authors: ["Xavier Camier"]
date: 2020-04-07T16:38:30+02:00
tags: ["Web","Tools"]
images: ["web.jpg"]
draft: false
---

## Goal: to remember how this site is built

To build this web site I use [Hugo](https://gohugo.io/). Hugo is a static site generator built in go. It is free, easy to understand and highly configurable. In addition to the egine you can download templates to have quickly a look'n feel that suits your need. The posts are written in markdown which is very handy to perform quick formatting.

As all the content is text based, it is easy to manage versions, to collaborate and to transfer the site from one machine to another. 

### First steps

Note: my environment is OSX 10.11

- Install of Hugo: [Quick start](https://gohugo.io/getting-started/quick-start/)
- Install of the theme: this website uses a theme called ["chunky-poster"](https://themes.gohugo.io/hugo-theme-chunky-poster/)

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
cd Development
hugo new site devExplorerBlog
cd devExplorerBlog
git init
git submodule add https://github.com/puresyntax71/hugo-theme-chunky-poster.git themes/hugo-theme-chunky-poster
{{< / highlight >}}

Now I have everything I need build my site.

### Configuration

Note: as editor I use Visual Studio Code.

- Download of an extended configuration file from the [chunky poster theme github](https://github.com/puresyntax71/hugo-theme-chunky-poster/blob/master/exampleSite/config.toml) and replacement of the one in "devExplorerBlog" folder
- Update the configuration by editing "config.toml"
    - Change of the `base URL` to match my domain **TO DO**.
    - Change of the site title` to "Code & Technics"
    - Change of the `copyright` to my name / date of creation of the site
    - Change of the `author`: it's me :-)
    - Change of the `description`
    - Configuration of the `[params.social]` section. I've set the URL to match with my social networks.
    - For now I won't use the prismJS syntax highlighting and use Hugo's one. So I keep `[params.prismJS]` disabled. However, I've set the theme to `okaidia` in case I would change my mind
    - Change of the top right image displayed on the `home page` to:

        `"homepageImage = "/images/homepage-image.jpg"`

        Of course I had to copy the corresponding image in the devExplorerBlog/content/images folder. If the folder doesn't exist create it.

    - Creation of an index.md file in the image folder containing the following:

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
---
headless: true
---
{{< / highlight >}}
I have no idea what it is for !

### Creation of the authors

The theme handles multi authors. The feature is interesting because when an author will be set in a blog post using the following tag in the post header...

`authors: ["author name"]`

... a list of posts of the author will be built. To find this list all I have to do is to click the author name.

#### To use the feature:
- From the command line add 

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
hugo new authors/xavier-camier/_index.md
{{< / highlight >}}

- Edit the content of `_index.md` Set the name, the avatar. I don't have a twitter account so I keep the entry free. Below the 3 dashes I have added a short biography.

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
---
name: Xavier Camier
images: ["beffroi.jpg"]
twitter: ''
---

Hi it's me...
{{< / highlight >}}

- Copy to the author folder the avatar picture you've configured
- For any reason the template uses a basic page. I had to force the layout:
    Rename 

    `devExplorerBlog/themes/hugo-theme-chunky-poster/layouts/_defaults/single.html`

    to whatever you want. Then copy paste the `single.html` file located in

    `devExplorerBlog/themes/hugo-theme-chunky-poster/layouts/post`
    
    to 
    
    `devExplorerBlog/themes/hugo-theme-chunky-poster/layouts/_defaults`


Note: you have to repeat all the section for all the authors of the blog


### The about page

To built the about page, just create a `about.md` file in 

`devExplorerBlog/content/`


### Creation of an article

`hugo new posts/name-of-post.md`

Edit the header as follow

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
---
title: "title of post"
description: "test"
authors: ["Xavier Camier"]
date: 2020-04-07T16:38:30+02:00
tags: ["Web","Tools"]
draft: true
---
{{< / highlight >}}

Note: draft is set to true. When you are read to publish the post, set to false.

Below the header, use text formatted with markdown to write a blog post.

### Serving

To serve and have a look at what you are creating (including the drafts)

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
hugo server -D
{{< / highlight >}}

To generate the static site that will be ready to be uploaded to your host

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
hugo -D
{{< / highlight >}}

Output will be in `./public/`