---
layout: post
title: "Jekyll: Make it Multi-Lingual"
tags: foss
published: true
language: en
---

As you may have noticed, this blog has basic level of support of multilingualism. There're several plugins out there to help us creating multi-lingual jekyll sites, but I eventually decided to make it simple. This blog's multilingualism is achieved with liquid tags, front matters, also a amazing plugin called [jekyll-placeholders](https://github.com/ample/jekyll-placeholders).

Our objectives here are:
1. To enble publishing posts in different lanaguages, all by Jekyll's functionality, without javascript.
2. It should be an addition not a requirement, so it should be okay to publish posts in whatever and any number of languages.
3. It should be easy to navigate between languages.

What we can take advantages of:
1. We can add whatever we want as [Front Matter](https://jekyllrb.com/docs/front-matter/)
2. With [jekyll-placeholders](https://github.com/ample/jekyll-placeholders), any Front Matter could be used in [Permalink](https://jekyllrb.com/docs/permalinks/)
3. Front Matters are accessible in Liquid tags, this allows us to know what languages are available for a post in Layouts/Includes.

## Generate Posts of Languages

The Front Matter of this post is shown below:
```markdown
---
layout: post
title: "Jekyll: Make it Multi-Lingual"
tags: foss
published: true
language: en
---
```

As you can see, I specified the **language** entry, which contains "en", this means, this post is written in "en" (It doesn't matter what language it actually is, it's just a variable).

As for now, the post is only in English, if in the future I write another version in, for example "tw", then it'd become:
```markdown
---
layout: post
title: "Jekyll: Make it Multi-Lingual"
tags: foss
published: false
language: en
other_language_versions:
- jekyll-make-it-multilingual/2021-05-31-jekyll-make-it-multilingual.md=tw
---
```

A `other_language_versions` front matter is added, and it's in "path_relative_to_post=lang" format. This entry will be used by Liquid to generate buttons to navigate between language versions, I'll show how to achieve that in the next section.

And this is my post permalink:
```markdown
collections:
  posts:
    output: true
    permalink: posts/:title/:language
```

Thanks to [jekyll-placeholders](https://github.com/ample/jekyll-placeholders), I can reference the **language** Front Matter here, so when Jekyll compiles the site, this post would be `posts/2021-05-07-jekyll-make-it-multilingual/en.html`.

By the way, The reason why I decide to place language at the tail is, It'd much easier to select langugage by url, though my site'd be very easy to switch language by buttons, It's still a good thing to do.

## Show The Lanaguage Options

In my home layout, this is how my post items are rendered:
```html
{% raw %}
      <li>
          {%- assign date_format = site.moving.date_format | default: "%b %-d, %Y" -%} // My site is based on [Moving](https://github.com/huangyz0918/moving) theme
          <span class="post-meta"> // Show the date of the post
            {{ post.date | date: date_format }}
          </span>
          <a class="black-link post-link-layout" href="{{ post.url | prepend: site.baseurl}}"> // How it links to the acutal post page
            {{ post.title | escape }}
          </a>
          {%- if post.language -%} // If the post has **language** front matter
              <span class="language_tag">{{ post.language | upcase }}</span> // en -> EN
          {%- endif -%}
          {%- if post.other_language_versions.size > 0 -%} // If the post has **other_language_versions** front matter
            {%- for L in post.other_language_versions -%} // Iterate through all options
              {%- assign data =  L | split: "="  -%} // Split the entry, take jekyll-make-it-multilingual/2021-05-31-jekyll-make-it-multilingual.md=tw as example, data[0] will be jekyll-make-it-multilingual/2021-05-31-jekyll-make-it-multilingual.md and data[1] will be tw.
              <span class="language_option"><a href="{% link _posts/{{ data[0] }} %}">{{ data[1] | upcase }}</a></span> // We use **link** here, so Jekyll will do the job for us to get the actual link, data[1] is showing what language version the button leads to
            {%- endfor -%}
          {%- endif -%}
      </li>
{% endraw %}
```

Just after these steps, We can present posts in multiple languages.
 