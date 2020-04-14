---
title: "Customization of an Hugo Theme"
description: "How to perform basic modifications on a Hugo Theme"
authors: ["Xavier Camier"]
date: 2020-04-14T12:00:00+02:00
tags: ["Web","Tools","Tutorial"]
images: ["web.jpg"]
draft: false
---

I was quite happy of how the [Hugo Theme](https://themes.gohugo.io/hugo-theme-chunky-poster/) I use look like but I wanted to tailor it a bit so that it aligns more with what I had in mind when starting building that blog. For basic things it is not very difficult. Let's perform two basic examples:

- On the front page I want to have the possibility to set a custom description of the post
- On an article, I don't want to have the number of words count

### Basics

It is not a good idea to edit directly a theme. [In this post]({{< ref "how-this-site-is-built/index.md" >}}) I've explained how to reference a theme as a submodule. That allows not to have to version the theme with your sources and to benefit of the latest update of the theme. Modifying the theme directly would force you to version the modifications and you may encouter conflicts when updating. So how?

Let's have a look at the hugo folders organization:

{{< figure src="images/folderstruct00.png" >}}


- There is another `layouts` folder at the root of the project
- There is a `layouts` folder into the themes folder

How it works:

The Hugo engine first parses the `layouts` folder then parses the `layouts` folder included in the theme. You've got it: when you want to customize a theme, put your customized file at the into the `layouts` folder located at the root of your Hugo site.

Captain obvious here: you must respect the hierarchy of the theme folders in your "root layouts" folder.

### Example 1: modifying the front page cards

{{< figure src="images/card.png" >}}

I feel the content of the card is too busy. And it doesn't respect markdown formatting causing some display inconsistency. My goal is to replace that summary with a description I would provide.

#### Let's start

By having a look at the theme structure, we can see the `card.html` template is located into the `_default` folder.

{{< figure src="images/folderstruct01.png" >}}

Therefore, the first step to modify the card that is displayed in the front page will consist in:
- Creating the `_default` folder in the `layouts` folder located at the root of the project
- Copy/Pasting the `card.html` file from the theme to the `layouts/_default` folder located at the root of the project
=> now the hugo engine will use that file to render a front page card.

#### Let's read some code

{{< highlight html "linenos=table,hl_lines=4 17,linenostart=1" >}}
<div class="card h-100">
    {{ $page := . }}
    <a href="{{ $page.RelPermalink }}" class="d-block">
        {{- with $page.Params.images -}}
            {{- $images := . -}}
            {{- with $page.Site.GetPage "section" "images" -}}
                {{- with .Resources.GetMatch (strings.TrimPrefix "/images/" (index $images 0)) -}}
                    {{- $image := .Resize "700x350" -}}
                    <img data-src="{{ $image.RelPermalink }}" class="card-img-top mx-auto d-block" alt="{{ $page.Title }}">
                {{- end -}}
            {{- end -}}
        {{- end -}}
        <div class="card-body">
            <h4 class="card-title">{{ $page.Title }}</h4>
            <p class="card-text text-muted text-uppercase">{{ $page.Date.Format "January 2, 2006" }}</p>
            <div class="card-text">
                {{ $page.Summary | plainify }}
            </div>
        </div>
    </a>
</div>
{{< / highlight >}}

What we can see here is that `line 17`, a summary of the content is displayed. It is probably built based on the n first words of a post.

`line 4` is interesting because it seems using the `images` parameter of the page to display the card header. It's a good clue of how to create a parameter that could be used for the custom description.

#### Let's modify some code

Line 17 has to be modified as follow:

{{< highlight html "linenos=table,hl_lines=17,linenostart=1" >}}
<div class="card h-100">
    {{ $page := . }}
    <a href="{{ $page.RelPermalink }}" class="d-block">
        {{- with $page.Params.images -}}
            {{- $images := . -}}
            {{- with $page.Site.GetPage "section" "images" -}}
                {{- with .Resources.GetMatch (strings.TrimPrefix "/images/" (index $images 0)) -}}
                    {{- $image := .Resize "700x350" -}}
                    <img data-src="{{ $image.RelPermalink }}" class="card-img-top mx-auto d-block" alt="{{ $page.Title }}">
                {{- end -}}
            {{- end -}}
        {{- end -}}
        <div class="card-body">
            <h4 class="card-title">{{ $page.Title }}</h4>
            <p class="card-text text-muted text-uppercase">{{ $page.Date.Format "January 2, 2006" }}</p>
            <div class="card-text">
                {{ $page.Params.description | plainify }}
            </div>
        </div>
    </a>
</div>
{{< / highlight >}}
Code extracted from card.html

Now let's update the blog post with a short description:

{{< highlight go "linenos=table,hl_lines=3,linenostart=1" >}}
---
title: "How This Site Is Built"
description: "test description"
authors: ["Xavier Camier"]
date: 2020-04-07T16:38:30+02:00
tags: ["Web","Tools","Tutorial"]
images: ["web.jpg"]
draft: false
---
{{< / highlight >}}
Code extracted from the header of the reference blog post

#### Does it work?

Let's review the result on the site...

{{< figure src="images/updatedCard.png" >}}

It works !


### Example 2: removing information I don't need in a post

The screenshot below shows a blog post header

{{< figure src="images/defaultHeader.png" >}}

This blog is a technical blog. I don't feel knowing the reading time or the number of words will drive the decision to process a post now or later. Furthermore, as for any technical reading, the number of words doesn't illustrate how much time we need to understand what we read. Let's remove that information.

#### Let's start

Because of previous investigations, I know that blog posts are defined by the `single.html` template. By having a look at the theme structure, we can see the `single.html` file is located into the `_default` folder.

{{< figure src="images/folderstruct01.png" >}}

Therefore, the first step to modify the blog page display will consist in Copy/Pasting the `single.html` file from the theme to the `layouts/_default` folder located at the root of the project
=> now the hugo engine will use that file to render a blog post.

#### Let's review the code

{{< highlight html "linenos=table,hl_lines=5-6,linenostart=1" >}}
<div class="row justify-content-center">
    <div class="col-lg-8">
        <div class="meta text-muted mb-3">
            <p class="created text-muted text-uppercase font-weight-bold mb-1">{{ $page.Date.Format "January 2, 2006" }}</p>
            <span class="mr-2"><i class="fas fa-book-open mr-2"></i>{{ T "wordCount" $page.WordCount }}</span>
            <span><i class="fas fa-clock mr-2"></i>{{ T "readingTime" $page.ReadingTime }}</span>
        </div>

        <h1>{{ $page.Title }}</h1>

        {{ partial "authors.html" $page }}
    </div>
</div>
{{< / highlight >}}
We can see some interesting keywords here: "wordCount" and "readingTime"

#### Let's modify the code

We'll start by just removing the rows we don't want to be displayed and see if it's enough.

{{< highlight html "linenos=table,linenostart=1" >}}
<div class="row justify-content-center">
    <div class="col-lg-8">
        <div class="meta text-muted mb-3">
            <p class="created text-muted text-uppercase font-weight-bold mb-1">{{ $page.Date.Format "January 2, 2006" }}</p>
        </div>

        <h1>{{ $page.Title }}</h1>

        {{ partial "authors.html" $page }}
    </div>
</div>
{{< / highlight >}}
No reference to reading time or wordcount anymore.

#### Does it work?

Let's review the result on the site...

{{< figure src="images/updatedHeader.png" >}}

It works !

Extra benefit, some vertical space is saved !


### Conclusion

It is not that difficult to tailor an Hugo theme as long as you respect some conventions and understand the structure of the code. 

Note: to learn how to customize or to tailor themes, a good start point is to [download other themes](https://themes.gohugo.io/), to test them and to check their code.
