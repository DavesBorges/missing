
# 2022-10-21

I should add a search function with Lume's Pagefind plugin
(https://lume.land/plugins/pagefind/).

-- dz4k


# 2022-08-19

Got a proof-of-concept for postcss-literate. However, imported files seem not
to go through it.

Not a big problem, since our import tree is not that big anyway. We could live
without imports and just concatenate things.

Possible workflow: Whole repo is a Lume site. CSS is written in .css.md files.
These files are also pages on the site. CSS code is removed from them. A
.tmpl.ts file iterates over the collection that has these files and puts them
through PostCSS to generate the final artifact.

A snag with that workflow is that Lume doesn't provide a way to build just one
page. So, maybe the .tmpl.ts file should not use Lume collections, but read the
.css.md files directly, such that it can be invoked in a non-Lume context.

This is all for post-1.0 however. The manual updating of the docs is workable
for now.

-- dz4k


# 2022-08-18

i'm going to add a fullwidth utility... class="width:100%" or 
class="inline-size:100%"?

***

/ chota (https://jenil.github.io/chota/#features) has a grid system i could
derive inspiration from. i don't like all of it but there are some good things
in there

class="1 3s 5l" 1 col on desktop or tablet, 3 cols on phone, 5 cols on big

-- dz4k


# 2022-08-16

Updating docs is hard and I always forget something. Consider putting docs next
to code:

 - using npm:literate-postcss
 - using some tool that extracts comments from css

-- dz4k


# 2022-08-02

Neither basicgrid nor the flex utilities are good enough because layouts need
to adapt to device size and for any moderately sophisticated layout, that 
means media queries. I don't want missing.css to just be Tailwind but worse,
so `sm:flex-2` is off the table.

I'm writing this after needing to make two different sidebar layouts, and 
finding the one with custom CSS much easier to write. The one without is also 
simply broken on mobile.

Maybe just add a CSS Grid tutorial in the docs? In that case, find a way to 
achieve LoB with CSS.

What I wish existed on the Web:
  ~~~
  <section>
    <style>
      :scope {
        background: var(--box-bg); /* Adds columns to this section */
      }
    </style>

    <p>Lorem ipsum dolor sit amet...
  </section>
  ~~~

-- dz4k


# 2022-06-21

add an utility for all: initial.

-- dz4k

# 2022-06-12

Got the forms into somewhat of an acceptable state.

Removed a PostCSS plugin, trying to reduce build dependencies.

TODO add utilities for all display: values.

TODO Replace basicgrid with a set of generic flex utilities covering a large
amount of Flexbox. Basicgrid is just not flexible (ha!) enough.

TODO Make the s, m, l sizes configurable through CSS variables.

TODO Start a missing.css blog. It could be a microblog in this style, written
in one big YAML file.

I want to make a 0.0.1 release pretty soon. I'll do it when I have the
hyperscript.org website migrated to missing.css and looking good.

-- dz4k


# 2022-05-20

I hate forms.

There are so many ways to mark them up, and so many ways they can look. There
is no correlation between the way a form was marked up and the way the author 
wants is presented.

The legend element is broken.

I'm looking into what other CSS libraries do.

-- dz4k


# 2022-05-18

I finally got the Deno PostCSS build to work. Turns out that the CSS optimizer
CSSO was crashing because of invalid syntax.

I spotted the syntax error by pasting the built unminified CSS into an
[online validator]. I'd rather not have it crash on every syntax error though,
at least not without a helpful error message.

Integrate a validator into the build. A _very_ cursory search showed this:
<https://github.com/morishitter/postcss-validator>

[online validator]: https://jigsaw.w3.org/css-validator/

-- dz4k

# 2022-05-17

Idea for branching structure:

No `master` or `main` branch. Different projects use the default branch for
different purposes, which can be confusing. I don't want people to need to read
stuff just to send a PR.

The default branch is called `dev`. This means the default branch is the right
place to open PRs.

There is a `prod` branch, which is what's deployed to Netlify. To release a new
version, make a git tag and move the prod branch to it. In addition,
documentation fixes can be made directly against the prod branch.

Feature branches probably won't be used much, and most development will be
directly on the dev branch. This is because of the difficulty of merging CSS.

-- dz4k


# 2022-05-17

> - how to write docs?
I'm just writing them in markdown and putting `<dfn>` tags everywhere that I
can hopefully index somehow. I want any instance of something like
`` `.class` `` to link to where the class is defined.

I did something kind of like this with [denizaksimsek.com] with Lume, where I
preprocessed markdown to detect wiki-style links, made an index of what page
links where, and used that index in my template to generate backlinks.

I was wondering how to generate docs from code comments. I've been writing a
few small features docs-first lately and it's been great. I wonder if a
literate programming approach would be a good way to go.

CSS seems like a particularly good candidate for literate programming since
code doesn't have to be in sequence. However, I didn't find any tools for
literate programming in CSS and I don't feel like writing and maintaining one.

-- dz4k


# 2022-04-31

> - remove all :is, see what happens

removed all instances of :is and :where. nothing happened

-- dz4k
