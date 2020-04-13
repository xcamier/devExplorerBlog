---
title: "How This Site Is Built"
description: "Description of how I build the website using Hugo"
authors: ["Xavier Camier"]
date: 2020-04-07T16:38:30+02:00
tags: ["Web","Tools","Tutorial"]
images: ["web.jpg"]
draft: false
---

## Goal: to explain how this site is built

To build this web site I use [Hugo](https://gohugo.io/). Hugo is a static site generator built in go. It is free, easy to understand and highly configurable. In addition to the egine you can download templates to have quickly a look'n feel that suits your need. The posts are written in markdown which is very handy to perform quick formatting.

As all the content is text based, it is easy to manage versions, to collaborate and to transfer the site from one machine to another. 

The site will be hosted freely by github. It is convenient, free and requires few configuration steps described here below.

Thanks to github actions you can automate the site generation and publication on github.


### Creation of the project

Note: Environment is OSX 10.11

**On the computer**
1. Install of Hugo: [Quick start](https://gohugo.io/getting-started/quick-start/)

**On Github**

2. Create your project as described below

{{< figure src="images/githubcreate.png" >}}

    Note: to be considered as website to serve by github, the name of the site shall respect the tempate "yourSiteName.github.io"

    Points of care:
        - Make sure to make the site public
        - Make sure to create the default readme file, that will help later


3. Create a new branch called `source` 

{{< figure src="images/sourcebranch.png" >}}

    This is where the source of the site will be pushed. Github uses the master to publish the site and the branch of your choice (here called `source`) for the source code of the web site.

4. Make sure the `source` branch becomes the default one

- Go to the settings menu

{{< figure src="images/settingsmenu.png" >}}

- Select Branches then select the source branch as default branch and click update

{{< figure src="images/sourceasdefault.png" >}}

**On the computer**

5. Retrieve the site from github

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
git clone https://github.com/xcamier/siteName.github.io.git
{{< / highlight >}}
The git repository is initialized and checked out with the source branch.


### Creation of the hugo site

6. Create the site using the hugo `hugo create site` command

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
hugo new site siteName.github.io --force
{{< / highlight >}}

The `force` extra parameter allows to create the site in the already existing directory

7. Install of the theme: this website uses a theme called ["chunky-poster"](https://themes.gohugo.io/hugo-theme-chunky-poster/)

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
cd siteName.github.io
git submodule add https://github.com/puresyntax71/hugo-theme-chunky-poster.git themes/hugo-theme-chunky-poster
{{< / highlight >}}
The theme is retrieved and a submodule is created. This is interesting because the theme doesn't need to be pushed to github. It will be retrieved whenever you need it. Note that if you need to force the retrieval of the submodules, the command `git submodule update --init --recursive` should do the job.

Now you have everything you need build your site.

8. Let's not publish useless files

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
touch .gitignore
{{< / highlight >}}
This creates a file that will contain the files and folders to exclude from the git commit/push

Edit the file with the following content:

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
resources/_gen
.DS_Store
public/*
{{< / highlight >}}
.DS_Store is not useful if you are not on OSX.


### Configuration

Note: as editor I use Visual Studio Code.

9. Download of an extended configuration file from the [chunky poster theme github](https://github.com/puresyntax71/hugo-theme-chunky-poster/blob/master/exampleSite/config.toml) and replacement of the one in "devExplorerBlog" folder
- Update the configuration by editing "config.toml"
    - Change of the `base URL` to match the github URL: `https://yourgitname.github.io/siteName.github.io/`.
    - Change of the site title` to "Code & Technics"
    - Change of the `copyright` to my name / date of creation of the site
    - Change of the `author`: it's me :-)
    - Change of the `description`
    - Configuration of the `[params.social]` section. I've set the URL to match with my social networks.
    - For now I don't use the prismJS syntax highlighting and use Hugo's one. So I keep `[params.prismJS]` disabled. However, I've set the theme to `okaidia` in case I would change my mind
    - Change of the top right image displayed on the `home page` to:

        `"homepageImage = "/images/homepage-image.jpg"`

        Don't forget to copy the corresponding image in the `content/images` folder. If the folder doesn't exist create it.

    - Creation of an index.md file in the image folder containing the following:

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
---
headless: true
---
{{< / highlight >}}
I have no idea what it is for !


### Creation of the authors

The theme handles multi authors. The feature is interesting because when an author will be set in a blog post using the tag `authors: ["author name"]`. The hugo engine will create a list of posts of the author automatically. To find this list all I have to do is to click the author name.

10. Creation of an authors is as easy as creating a post

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
hugo new authors/xavier-camier/_index.md
{{< / highlight >}}
It's like creating a new post

- Edit the content of `_index.md` Set the name, the avatar. I don't have a twitter account so I keep the entry free.

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
---
name: Xavier Camier
images: ["youravatar.jpg"]
twitter: ''
---

Hi it's me...
{{< / highlight >}}
Below the 3 dashes you can add the biography of the author.

- Copy to the author folder the avatar picture you've configured
- For any reason the template uses a basic page. If you want to see the author:
    - Create a `_default` folder in the layouts folder
    - Copy/Paste the `single.html` file contained in
    `themes/hugo-theme-chunky-poster/layouts/post` to that new folder


### The about page

11. About page is also as easy as creating a post

To built the about page, just create a `about.md` file in `content/`.

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
---
title: "About"
date: 2020-04-07T12:41:54+02:00
draft: false
---
{{< / highlight >}}
No tags or picture for me.


### Creation of an article

12. Create your first post in command line

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
`hugo new posts/name-of-post.md`
{{< / highlight >}}


Once created, edit the header of the post as follow

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
Keep draft as true until your post is ready to be published

Below the header, use text formatted with markdown to write a blog post.


### Testing

To serve and have a look at what you are creating (including the drafts)

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
hugo server -D
{{< / highlight >}}
Read what is displayed on the screen to access your local site from your favorite browser


### Automating the publication

**On GitHub**

In order to automate the site building and pushing to the master branch, you can use a continuous integration of your choice as explained in [that post](https://jellis18.github.io/post/2017-12-03-continuous-integration-hugo/) or you can use Github actions. It looks easier to me and thanks to the script explained [here](https://github.com/peaceiris/actions-hugo) it is very quick to configure.

13. Go to the Actions section 

- Click "Setup a workflow yourself"

{{< figure src="images/actionsmenu.png" >}}

- Name your workflow `action`
- Earse the default script
- Copy/Paste the following code

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
name: Hugo_Site_Publishing

on:
  push:
    branches:
      - source

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.68.3'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: master  # deploying branch
{{< / highlight >}}
It's almost as in the [example](https://github.com/peaceiris/actions-hugo#%EF%B8%8F-create-your-workflow).

The interesting fields in our case are the "branches" => `source`. As explained earlier it's where we store the site code on Github. Also the "publish_branch:" `master` where the site generated in `public` with the command `hugo --minify` will be pushed. 

- Click the `Start commit` button

Note: when you go back to the actions section, you can see the actions that have been triggered and the result of the actions. That is helpful for troubleshooting.

{{< figure src="images/workflowsresults.png" >}}


### Serving

14. Configure the serving on Github

- Go to the settings menu

{{< figure src="images/settingsmenu.png" >}}

- In the `options` section, activate the serving of the site. Note the URL. 

{{< figure src="images/serving.png" >}}
Note the URL indicated by Github


### If you want to generate the site locally

**On the computer**

15. Generate the static site that will be ready to be uploaded to your host

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1" >}}
hugo -D
{{< / highlight >}}
Output will be in `public/`


