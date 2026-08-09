+++
title = 'Making a blog website with Hugo'
date = 2026-08-09T15:48:50-04:00
draft = false
+++

This post works through my 1-day process of installing Hugo, configuring it with a custom theme, and making _this_ blog post.

<!--more-->

# What is Hugo?

[Hugo](https://gohugo.io/) is known as a _static site generator_. It is used to make a wide assortment of different websites, but it seems very popular to use in this exact case I am today- making blogs.

Hugo was written in Go and unlike usual websites that dynamically generate the page whenever someone visits it, Hugo generates it ahead of time. The HTML is fully generated ahead of time. This makes it very nice to use with github pages.

The ability to write posts in markdown makes the speed, and ease of use for blogging miles easier and takes much less time. Another option that people use often for github pages is [Jekyll](https://jekyllrb.com/). I looked at it once and decided I didn't want to install [Ruby](https://www.ruby-lang.org/en/) :P.

# The Process

I installed Hugo on my WSL2 Debian instance and immediately went to the documentation and read the [Quick-Start](
  https://gohugo.io/getting-started/quick-start/) page. I found the quickstart a bit weird as I wanted to make my own theme so telling the person to clone _Ananke_ off-rip was kind of weird. I ended up just asking ChatGPT to give me a quick-start and it told me to generate a theme using `hugo new theme (name)` in my terminal which was **not** required at all.

If you are deciding on making your own blog using Hugo, and want to create your own theme, you only need the base file structure. There is no need for a separate theme module. The general file structure isn't that difficult to understand. This is my structure:

![File Structure](file-structure.png)

I don't know what `archetypes`, `assets`, or `data` do. Who needs those though? I didn't.

Couple things to note about this file structure:
- `content/posts/` is where all the posts go. Each post can be a separate folder where all assets/images reside, as well as the main `index.md` file (it needs to be named index.md, trust me bro).
- `_defaults/baseof.html` is like the main HTML file, it contains all the links to stylesheets and the general structure of the website.
- `list.html` aswell as `single.html` are separate elements that get placed into the `baseof.html` file on a loop. The `list.html` is the list of posts under my full post list page. `single.html` is the HTML that makes this current page.
- The _partials_ are almost components as well, similar to the `list.html` and `single.html` but it's even smaller in scale. In my case, `icon.html` is used to only generate the icons on the status element at the bottom of these pages. The github/youtube icons specifically.

# Icons

Icons were a little interesting and made me learn something new about CSS/HTML. So interesting in fact that I'm dedicated a whole section to them.

```html
<svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor" aria-hidden="true">
  <path d="M12 .5C5.73.5.5 5.73.5 12c0 5.08 3.29 9.39 7.86 10.91.57.1.78-.25.78-.55 0-.27-.01-1.16-.02-2.11-3.2.7-3.88-1.36-3.88-1.36-.52-1.33-1.28-1.68-1.28-1.68-1.04-.71.08-.7.08-.7 1.15.08 1.76 1.18 1.76 1.18 1.03 1.76 2.7 1.25 3.35.96.1-.75.4-1.25.73-1.54-2.55-.29-5.24-1.28-5.24-5.68 0-1.25.45-2.28 1.18-3.08-.12-.29-.51-1.46.11-3.04 0 0 .96-.31 3.15 1.18a10.9 10.9 0 0 1 5.74 0c2.19-1.49 3.15-1.18 3.15-1.18.62 1.58.23 2.75.11 3.04.74.8 1.18 1.83 1.18 3.08 0 4.41-2.7 5.38-5.27 5.67.42.36.78 1.08.78 2.17 0 1.57-.01 2.83-.01 3.22 0 .3.2.66.79.55A10.51 10.51 0 0 0 23.5 12C23.5 5.73 18.27.5 12 .5z"/>
</svg>
```
*You'll most likely have to scroll a lot for this code snippet...*

This HTML snippet defines the SVG _paths_ for what to render... I had no idea this was possible. There might be a better way to do this but, this works so I'll stick with it.

Together in junction with this icon-svg-rendering method, I specified some stuff in my `hugo.toml` file:

```toml
[[params.social]]
  name = "github"
  url = "https://github.com/komidan"

[[params.social]]
  name = "youtube"
  url = "https://youtube.com/@komidan_"
```

To render the icon, I'm just reading the name and converting it to the SVG element. As I was making this, I was originally going to just leave them as plain text _youtube_ and _github_. I was certainly a fan of this method.

# Styling

Styling Hugo is like styling any website. It's a lot of CSS- ~~boring~~ amazing CSS (it wasn't that boring, but I for sure did use Claude to make it quicker...). If you can't tell by my websites obvious [Gruvbox](https://github.com/morhetz/gruvbox) theme, I like gruvbox. I use Gruvbox colors everywhere- terminal, desktop environment, browsers, helix, zed, codium. Point is, if it has gruvbox themeing capabilities, I will certainly try to get gruvbox.

Having worked with CSS before for a [waybar](https://github.com/Alexays/Waybar) configuration I already had the palette ready to copy and paste, I just had to tell Claude to follow it. As for inspiration for the website, I was working on a system customizing [KDE Plasma](https://kde.org/plasma-desktop/) a bit and made my environment similar to MacOS with the top bar and a smaller icon-based task bar. My navigation bar and smaller bar on top and bottom of the page follow this. The posts were just a random _"make them cards!"_ thought.

The more technical side of the styling was styling these pesky code snippet elements. Since Hugo is a static site generator, they can't be dynamically altered. Hugo has many built-in themes for syntax highlighting. To generate the CSS file you can run something very similar to this:

> `hugo gen chromastyles --style=gruvbox > static/css/syntax.css`

After that is generated, you just include it as a regular css file in `baseof.html`. This however, does not change the container element surrounding the snippet text itself. To change that I have to do this:

```css
/* inline code (not in a fenced block) */
.post-content :not(pre) > code {
  background: var(--bg-soft);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 0.15rem 0.4rem;
  font-size: 0.9em;
  font-family: "SF Mono",  b
  Consolas, monospace;
}
```

And for full snippets:

```css
/* full-blocks */
.post-content .highlight {
  margin: 1.5rem 0;
  padding: 0.75rem 1.25rem;
  border-left: 3px solid var(--accent);
  background: var(--bg-soft);
  color: var(--fg-muted);
  border-radius: 0 8px 8px 0;
}

.post-content .chroma {
  overflow-x: auto;
  font-size: 1.3rem;
  background: none;
}

.post-content .chroma pre {
  margin: 0;
}

.post-content .chroma code {
  background: none;
  border: none;
  padding: 0;
}
```

It definitely felt a bit complicated at points, but I'm very happy with the current state of my blog styling. There might be some things that need to be fixed over time but I would rather keep this very simple and not something large to maintain. I probably won't be making an insane amount of blog posts anyway.

# Conclusion

Hugo is great for personal blogs or websites hosted on github pages. Generating content statically makes load times quick and writing in markdown is saving a ton of time. I fully recommend trying this yourself if you are interesting one evening. And if you don't want to spend 5 hours on it (excluding writing this) like me, use an already [built theme](https://themes.gohugo.io/).

This is my first day, so I've still got much to learn, and this blog can serve as a look-back at my progress.

- - -

I love Maya.
> \-komidan

