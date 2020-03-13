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


# Theme configure
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



