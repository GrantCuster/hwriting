---
date: 2020-07-30T10:34:10
title: "Automadraw"
---

{{< 
figure src="/images/automadraw-1596131469.gif" 
>}}

[Automadraw](https://automadraw.constraint.systems) is a new app I made for my [Constraint Systems](https://constraint.systems) project. It lets you draw and evolve your drawing using cellular automata using two keyboard controlled cursors.

## What is it for

I think there are two main uses for Automadraw:
1. Get more familiar with the cellular automata (Conway's Game of Life and Langton's Ant) that it runs. You can quickly experiment with lots of different patterns.
2. Draw something collaboratively with the automata. The interaction design aims to make working with the automata intuitive. These design techniques (two cursors, keyboard controls) could be applied to a wide range of creative apps.

## Two cursors

I had originally planned to use just one cursor, and have it shift between draw mode and "act" (run automata) mode. As I experimented I found that usually for act mode I wanted to cover a large area and draw mode a smaller one. Having to resize when switching between modes ruined the flow, so I split the cursors up. 

Splitting them up opened up some new possibilities. I realized I could set it up so that I could use each cursor's actions (draw or act, respectively) regardless of which one was in focus. This set up a couple of interactions I really liked:

{{< 
figure src="/images/gif-2020-07-30_13-53-52@2x-1596131748.gif" 
title="Sweeping: draw some lines then use a long, narrow act cursor to sweep over the lines, running Game of Life over each sweep step. This usually produces intricate symmetrical designs that really feel like they're evolving through each sweep."
>}}

{{< 
figure src="/images/gif-2020-07-30_13-58-43@2x-1596132012.gif" 
title="Active environment: resize the act cursor over a large area, use the draw cursor and have it move in and out of the act area as the automata is run. The act area becomes an environment where different rules apply. It feels like a physics or chemistry simulation."
>}}

This set-up is uniquely suited to keyboard cursor controls, where each cursor's position is fully visible and fully predictable (versus a touch interface where you would have to use multiple fingers and the fingers themselves would obscure your view of the changes taking place). I use Vim-like keyboard controls because I honestly prefer them. My suspicion is that they may enable modes of interaction other methods do not. I was happy to find an interaction that fit them so well. I'm looking forward to seeing how even more multiple cursors feel in future experiments.

([Stamp](https://stamp.constraint.systems) is a different example of the possibilities of multiple cursors: two cursors across two canvases.)

## Keyboard events

Part of the reason the two cursor interaction is interesting is because of an accident of keyboard event handling. A lot of the Constraint System experiments let you hold down multiple keys. This is tricky to handle in Javascript for everything except modifier keys. The main issue is that if you're holding down one key, and start holding an additional one, the new one will take over the `keyDown` event. The solution is to make a keymap object, store each key on `keyDown` and remove it on on `keyUp`. You then use the keymap object for the source of truth about what is pressed on each `keyDown` event.

This technique mostly just works, but there turns out to be an issue, arguably a bug, that makes things like the "sweep" technique I discussed above possible. If you are pressing one key, add another key, then let up on the second key, `keyDown` events stop firing. For Automadraw, this behavior enables this interaction:

- Hold down 'a' to run automata, press a direction key to move the act cursor. When you let up on the direction key the automata will pause running... until you press a direction key again. Using this technique you can run "sweeps", moving the act cursor across a set of pixels, automatically running the automata once each step.

This interaction was a happy accident, and I'm looking forward to thinking about how to expand and support it more in future experiments.

## Limitations and future possiblities

I had been wanting to experiment with cellular automata and a drawing app for a long time. For this experiment, I needed to really scope things down in order to get started. I restricted the drawing app colors to 1-bit (on or off). This usefully limited the number of cellular automata I could use and the number of interactions I needed to support. I also made the app 'pixels' large, at 16 actual pixels. This makes drawing quick and the automata actions more legible, but also restricts the fidelity of the final image. Someday I would like to build a cellular automata app more focused on image editing, where you could evolve parts of an image at a higher fidelity. That would also involve using automata that use color information, there are some interesting examples of those in [this CA Lab demo video](https://www.youtube.com/watch?v=lyZUzakG3bE).

## Code

The code for Automadraw is [avaliable on github](https://github.com/constraint-systems/automadraw).

### Slowly recreating React

I built the early Constraint Systems experiments using React, but have moved off of it to vanilla Javascript for the most recent ones. I do find myself recreating a lot of the set-up of React. I've found out firsthand that a lot of the React boilerplate I questioned is in there to work around the constraints of Javascript itself. I may switch back to React sometime, but right now I'm still enjoying experimenting on my own. It is also true that a lot of the benefits of React don't mesh well with HTML canvas, which is where most of the action for this app takes place.

### ES6 modules

This was the first project where I used ES6 modules. It was nice to be able to organize the code into sections like `keyboard` and `state`. I'll continue to use them and refine my organization going forward. Maybe someday I'll have a true base starter kit I can reuse across projects.

### Canvas compositing

One switch I've made that I've been very happy with, is moving from rendering multiple canvas DOM elements on top of eachother, to placing only one canvas on the dom and compositing the different layers (in this case: `cursor`, `grid`, `art`) on to the DOM layer for each render. My rendering code is a little knotty, but it still feels a lot cleaner than stacking the canvases in the DOM.
