# After… no, no, ::before… wait…

![css][css]

Is it getting old for this crusty JS developer to keep venturing into the CSS
world for these posts? :)

Here’s a quick rant. And I think most people can probably agree it was a screw-
up to land how we did.

## Pseudo-CSS

Have you heard about [CSS pseudo-elements][1] `::before` and `::after`? If not,
or if you’re not already intimately familiar with them, what the heck are they?

Well, “pseudo” tells you right off the bat they’re probably more “virtual” than
“real”. What they’re designed to do is let you target for CSS styling some
special types of elements that don’t *actually* exist directly in your markup.
These special elements are virtually part of your document, even if they don’t
explicitly appear in your actual document structure.

What `::after` and `::before` are used for is to target the virtual “last child”
or “first child” of the container you apply the rules on. No, not the actual
first or last child, but a virtual one that’s there only if you choose to style
it, otherwise it’s a silent phantom.

Example:

    <style>
    #container { background-color:yellow; }
    #container::before { content:"!!!!! "; font-style:italic; }
    #container::after { content:"!!!!!"; font-weight:bold; }
    </style>
 
    <div id="container">I am not the only text in this box</div>

<style><!--
#container_ex1_inline::before { content:"!!!!!"; font-style:italic; }#container_ex1_inline::after { content:"!!!!!"; font-weight:bold; }
--></style>
<p id="container_ex1_inline" style="background-color: yellow;">I am not the only text in this box</p>

Cool, huh?

The purpose of the `content` rule in pseduo-elements is to add flourishes of
visual-decoration from your CSS, as presentation-only content, rather than
cluttering up your markup with presentation stuff. For instance, you might add
“external link” marker icons after your external links, or add stylized
quotation marks around a block-quote element, etc.

**NOTE:** You may see it recorded as either `::after` or `:after`. Technically, 
pseudo-elements and pseudo-selectors are supposed to switch to `::` instead of 
`:`. In most browsers, either works. I use `::` here since it’s the future!

## After what?

If you’re paying attention, though, `::before` and `::after` have a strange
semantic. If you’ve been following my recent rants on CSS, you know I have [very
strong opinions about CSS and semantics][2].

The word “before” and “after” indicate to most people that the content you’re
adding would be strictly before, or after, the element they’re styled against.
That is, they’d be strictly siblings to our container.

But what’s really happening is we’re revealing and styling virtual children of
our container, both in the virtual first-child position, and the virtual last-
child position.

Yeah, “after” doesn’t mean “after”, it means “at the very end of”. **Sigh.**
More semantic *screw-ups*. This seems to be happening a lot.

We already have a strong precedent in the JS world for adding some child to the
end of an element after all other children, or inserting some child before all
other children. In the world of JS frameworks (jQuery, etc), or even just in the
built-in native DOM API, we call something like `parent.appendChild(child)` to
append a child to the end of the children list of a parent container. It might
have been nice(r) if CSS had named `::after`instead `::append` or `::append-
child` to give us a better semantic.

What about `::before`. Well, the native DOM API doesn’t have a `prependChild()`,
so we have to do the more round-about
`parent.insertBefore(child,parent.firstChild)`. Ugh. JS frameworks thankfully
gave us things like `prepend()` to do the task. So the nice(r) counter-part in
CSS could/should have been `::prepend` or `::prepend-child`.

## ::repeat-mistakes:no

This whole semantically bizarre CSS thing is frustrating, not in the one
instance but in the fact that it happens a lot. But, I guess that’s just the
life of a web developer.

Still, I think if we call out such *mistakes*, maybe we can, as time goes on,
see less of them. Hopefully!?

What do you think? Was CSS right to call it `::after`? Or, should they add a
more semantic alias like `::append` and deprecate the busted one? Or should I
just `::get-over-it`?

[1]: https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements
[2]: http://blog.getify.com/html-vs-css-semantics/

[css]: img/shutterstock_145488154-660x380.jpg