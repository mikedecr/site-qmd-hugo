# quarto x hugo site

very WIP.

## Main idea

Source code for literate posts in `.qmd`.
Render all `.qmd` to `.md`.
Website builder handles `.md` to `.html`.

Since Quarto hit the scene, many users ported their blogs to Quarto's bundled website building framework, centered around Bootstrap / Bootswatch themes.
But it isn't necessary to hook to this site generation framework.
Quarto is at its core "just" a literate document compilation framework, and we can pass its output to other site generator frameworks.

## Thoughts: separation of config and config surgery

Many of these static site generators want you to include `yaml` or `toml` front matter at the page level.
Some of these configs are specific to the document behavior, and some of them are meant to bridge the document and the surrounding site generation framework.
This mixing of responsibilities is, to me, a bit smelly.
What I would ideally prefer is some way to encapsulate the quarto-stuff in the `.qmd`, and if there are extra parameters that the site generator needs, that should live somewhere else.

To Quarto's credit, their website project framework is pretty good about separating these things.
Documents control document params, and if there are website variables that need to be configured, those can go into local `index` files or local `_quarto.yml` files.
Quarto also lets you scope build routines to specific "profiles".

Hugo is, from what I can tell, a bit less careful about this.
So, here something I am considering: separate quarto config and web config into separate files, and then either _during `qmd compilation`_, or as some kind of site build hook, inject the variables another file.
This is unfortunately _work_, but might be good exercise to build a scripting framework for it.
