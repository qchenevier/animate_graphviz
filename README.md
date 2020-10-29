# Animated Graphviz

Small [static html page](https://qchenevier.github.io/animate_graphviz/) to animate a [Graphviz](https://graphviz.org/) `dot` file, based on [d3-graphviz](https://github.com/magjac/d3-graphviz).


## Usage

### User interface

- Go to https://qchenevier.github.io/animate_graphviz/
- Load your `dot` file in the page using the `Choose file` button
- Animate your graph step by step thanks to the `Next step` and `Restart animation` buttons
- At any time you can save the `svg` rendering using the `Save SVG` button


> ☝️ The frame size of the `svg` is approximately the window size when the `svg` is rendered. If the `svg` frame is too small or too big, resize the browser window and restart the animation.

### `dot` file syntax

This script uses a new property — `animate` — to show or hide nodes/edges at each animation step. Using regex, the `animate=LIST_OF_STEPS` property is replaced before the rendering by [d3-graphviz](https://github.com/magjac/d3-graphviz):
- The tag is replaced by `style=invis` when the current step does not belong to the `LIST_OF_STEPS`, so that the node/edge is hidden.
- The tag is removed if it belongs to the `LIST_OF_STEPS`, so that the node/edge is shown.

The `LIST_OF_STEPS` is a comma-separated list of singletons or ranges. For example, all those steps specs are equivalent:
- `1,2,3,4`
- `1-4`
- `1-3,4`
- `1,2,3-4`

> ☝️ No spaces allowed in the `LIST_OF_STEPS`: only numbers, commas & hyphens.

For example: This node will be displayed from step 2 to step 5 in the animation:
```graphviz
node_1 [
  label="This is a node"
  style="dotted"
  animate="2-5"
]
```
For the other steps, the node will remain hidden.

> ☝️ It is only a regex-based replacement (not a proper parsing & modification of the graph) so be sure that your `animate` tag is written **after** other `style` tags in the node/edge specification. Otherwise, the graphviz parser won't consider it.
