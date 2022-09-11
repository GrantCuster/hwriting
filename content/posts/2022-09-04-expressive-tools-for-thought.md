---
date: 2022-09-04T09:58:24
title: "Expressive tools for thought"
published: false
---

I'm excited for all the energy around tools for thought. Some notes on my current thoughts (probably to be revised in future entries).

## Blocks as the basic unit

Blocks as a basic, contained, and usually addressable unit feels to me "right". You can see it in Notion and Roam and many others.

I think the collapsible block (block that can have children) is also an essential piece as well. This is in Roam and Logseq (and Workflowy!). It's not in Notion or Obsidian as the default, and I miss it there.

The nested block structure makes a tree. I think one of the best parts of the tree structure is how it lends itself to restructuring. Move the top-level item and you move the children along with it. You can organize your writing at the top-level, or you can drill down into an item and reorganize within that. That feels right to me. It's notecard reorg, but even more flexible.

Trees are exclusively hiererchical and sometime relationships are not. This is where hyperlinks come in. And Roam did a great job of showing the possibilities here, with instant create and backlinks. With links + nested blocks you can have hierchical structure while also making these associative jumps. This seems like the right mix. I'm not sure we've cracked the best way to present it yet, I still get stressed trying to make sure I figure out the right link/category naming conventions.

## Blocks as individually addressable

Connected to this is the possibility of addressing indivdual blocks, whether creating links or something more like transclusion. Nested blocks plus addressing blocks seems to me the closest we've got to the promis of "what computers are good at" being marshalled for our own ends.

### Naming

Technically, the individually addressable blocks are interesting. The way I know to do it is to assign each one a uuid, which can be created in isolation with a strong guarantee that it won't collide with other individually created ids. This is cool. It helps with mutliplayer, it helps with simplified/contained creation.

With uuids we can have guaranteed unique ideas for all your bullet points.

But we've still got a naming issue. How do you refer to a block when you link to it? The uuid does not exactly stick in the mind. But it's also too much of a burden to ask you to name or tag each one of your bullet pointss. Use a section of the text maybe? Or bring up some fuzzy search interface that makes the linking easy -- still it's difficult to zero in on what in that bullet is useful important (say you wanted a zoomed out structural view, for example). Maybe machine learning bassed summarization helps here.

## Expressiveness

My current hot-take is that expressing yourself is intertwined with thinking, and none of the tools so far have paid enough attention to this aspect. I'm fascinated by the aesthetic college class notes culture around Notion, but I also find Notion's rules so limiting in expressiveness. Especially compared to the "older web" where I most often think of tumblr and how much room to make a genuinely unique blog structure there was (combined, interestingly, with the guardrails of the feed).

### Website-builders

I think expressivity has been under-addresssed. I also think html and CSS have advanced to the point where we can give users a subset
