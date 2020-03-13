# blog
Personal blog with [Jekyllrb](https://jekyllrb.com/) on Github pages. 

This package contains
* Raw blog contents in ``_post``. 
* Jekyllrb configurations. 

# Resources
* Git hub repostiory - https://github.com/hpxstarry/hpxstarry.github.io
* Personal blog website - https://hpxstarry.github.io/


# Website development - FAQ
## How to configure website (layout, theme)?
https://jekyllrb.com/docs/pages/

We are using theme chirpy now. Follow below wiki to update config. 
https://jekyll-themes.com/chirpy/#installing

## How to add table of contents?
https://github.com/allejo/jekyll-toc

## How to test
* jekyll build && jekyll serve --watch

## How to deploy
* jekyllrb build && git push

# Write blog - FAQ
## How to include image
1. Put it under ``assets/images``
2. Add ``![image](/assets/images/your_image.png)`` into your blog.


# Theme  configure

We are using theme chirpy now. Follow below wiki to update config. 
https://jekyll-themes.com/chirpy/#installing

## Customize the favicon

In [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/), the image files of [Favicons](https://www.favicon-generator.org/about/) are placed in `assets/img/favicons/`. You may need to replace them with your own. So let's see how to customize these Favicons.

Whit a square image (PNG, JPG or GIF) in hand, open the site [*Favicon & App Icon Generator*](https://www.favicon-generator.org/) and upload your original image.

![upload-image]({{ "/assets/img/sample/upload-image.png" | relative_url }})

Click button <kbd>Create Favicon</kbd> and wait a moment for the website to generate the icons of various sizes automatically.

![download-icons]({{ "/assets/img/sample/download-icons.png" | relative_url }})

Download the generated package, unzip and delete the following two from the extracted files:

- browserconfig.xml
- manifest.json
 
Now, copy the rest image files (`.PNG` and `.ICO`) to cover the original one in folder `assets/img/favicons/`.

Lastly, don't forget to rebuild your site so that the icon becomes your custom edition.



# Write a blog

## Naming and Path

Create a new file named with the format `YYYY-MM-DD-title.md` then put it into `_post` of the root directory.

## Front Matter

Basically, you need to fill the [Front Matter](https://jekyllrb.com/docs/front-matter/) as below at the top of the post:

```yaml
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORIE, SUB_CATEGORIE]
tags: [TAG]     # TAG names should always be lowercase
---
```

> **Note**: The posts' ***layout*** has been set to `post` by default, so there is no need to add the variable ***layout*** in Front Matter block.

- **Timezone of date**

    In order to accurately record the release date of a post, you should not only setup the `timezone` of `_config.yml` but also provide the the post's timezone in field `date` of its Front Matter block. Format: `+/-TTTT`, e.g. `+0800`.

- **Categories and Tags**

    The `categories` of each post is designed to contain up to two elements, and the number of elements in `tags` can be zero to infinity.

    The list of posts belonging to the same category/tag is recorded on a separate page. The number of such *category*/*tag* type pages is equal to the number of `categories`/`tags` for all posts, they must match perfectly. 

    let's say there is a post with front matter:
```yaml
categories: [Animal, Insect]
tags: bee
```

    then we should have two *category* type pages placed in folder `categories` of root and one *tag* type page placed in folder `tags`  of root:
```terminal
jekyll-theme-chirpy
├── categories
│   ├── animal.html
│   └── tutorial.html
├── tags
│   └── bee.html
```
    
    and the content of a *category* type page is
```yaml
---
layout: category
title: CATEGORY_NAME        # e.g. Insect
category: CATEGORY_NAME     # e.g. Insect
---
```

    the content of a *tag* type page is
```yaml
---
layout: tag
title: TAG_NAME             # e.g. bee
category: TAG_NAME          # e.g. bee
---
```

    With the increasing number of posts, the number of categories and tags will increase several times!  If we still manually create these *category*/*tag* type files, it will obviously be a super time-consuming job, and it is very likely to miss some of them(i.e. when you click on the missing `category` or `tag` link from a post or somewhere, it will complain to you '404'). The good news is that we got a lovely script tool to finish the pages creation stuff: `tools/init.sh`. See its usage [here]({{ "/posts/getting-started/#option-1-built-by-github-pages" | relative_url }}).

## Table of Contents

By default, the **T**able **o**f **C**ontents (TOC) is displayed on the right panel of the post. If you want to turn it off globally, go to `_config.yml` and set the variable `toc` to `false`. If you want to turn off TOC for specific post, add the following to post's [Front Matter](https://jekyllrb.com/docs/front-matter/):

```yaml
---
toc: false
---
```


## Comments

Similar to TOC, the [Disqus](https://disqus.com/) comments is loaded by default in each post, and the global switch is defined by variable `comments` in file `_config.yml` . If you want to close the comment for specific post, add the following to the **Front Matter** of the post:

```yaml
---
comments: false
---
```


## Code Block

Markdown symbols <code class="highlighter-rouge">```</code> can easily create a code block as following examples.

```
This is a common code snippet, without syntax highlight and line number.
```

## Specific Language

Using <code class="highlighter-rouge">```Language</code> you will get code snippets with line Numbers and syntax highlight.

> **Note**: The Jekyll style `{% raw %}{%{% endraw %} highlight LANGUAGE {% raw %}%}{% endraw %}` or `{% raw %}{%{% endraw %} highlight LANGUAGE linenos {% raw %}%}{% endraw %}` are not allowed to be used in this theme !

```yaml
# Yaml code snippet
items:
    - part_no:   A4786
      descrip:   Water Bucket (Filled)
      price:     1.47
      quantity:  4
```

#### Liquid codes

If you want to display the **Liquid** snippet, surround the liquid code with `{% raw %}{%{% endraw %} raw {%raw%}%}{%endraw%}` and `{% raw %}{%{% endraw %} endraw {%raw%}%}{%endraw%}` .

{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}

## Learn More
For more knowledge about Jekyll posts, visit the [Jekyll Docs: Posts](https://jekyllrb.com/docs/posts/).




# Text and graphics



## Titles

***
# H1

<h2 data-toc-skip>H2</h2>

<h3 data-toc-skip>H3</h3>

#### H4

***

## Paragraph

I wandered lonely as a cloud

That floats on high o'er vales and hills,

When all at once I saw a crowd,

A host, of golden daffodils;

Beside the lake, beneath the trees,

Fluttering and dancing in the breeze.

## Block Quote

> This line to shows the Block Quote.

## Tables

|Company|Contact|Country|
|:---|:--|---:|
|Alfreds Futterkiste | Maria Anders | Germany
|Island Trading | Helen Bennett | UK
|Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy

## Link

[http://127.0.0.1:4000](http://127.0.0.1:4000)


## Footnote

Click the hook will locate the footnote[^footnote].


## Image

![Desktop View]({{ "/assets/img/sample/mockup.png" | relative_url }})


## Inline code

This is an example of `Inline Code`.


## Code Snippet

### Common

```
This is a common code snippet, without syntax highlight and line number.
```

### Specific Languages

#### Console

```console
$ date
Sun Nov  3 15:11:12 CST 2019
```


#### Terminal

```terminal
$ env |grep SHELL
SHELL=/usr/local/bin/bash
PYENV_SHELL=bash
```

#### Ruby

```ruby
def sum_eq_n?(arr, n)
  return true if arr.empty? && n == 0
  arr.product(arr).reject { |a,b| a == b }.any? { |a,b| a + b == n }
end
```

#### Shell

```shell
if [ $? -ne 0 ]; then
    echo "The command was not successful.";
    #do the needful / exit
fi;
```

#### Liquid

{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}

#### HTML

```html
<div class="sidenav">
  <a href="#contact">Contact</a>
  <button class="dropdown-btn">Dropdown
    <i class="fa fa-caret-down"></i>
  </button>
  <div class="dropdown-container">
    <a href="#">Link 1</a>
    <a href="#">Link 2</a>
    <a href="#">Link 3</a>
  </div>
  <a href="#contact">Search</a>
</div>
```

**Horizontal Scrolling**

```html
<div class="panel-group">
  <div class="panel panel-default">
    <div class="panel-heading" id="{{ category_name }}">
      <i class="far fa-folder"></i>
      <p>This is a very long long long long long long long long long long long long long long long long long long long long long line.</p>
      </a>
    </div>
  </div>
</div>
```


## Reverse Footnote

[^footnote]: The footnote source.
