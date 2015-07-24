# Stop Writing JavaScript Frameworks
Slides: http://bit.ly/zf-preso-1

Maybe more accurate: Start writing orthogonally composable units of HTML/CSS/JS.

Originally, web development was much harder because there was no consistent model for browsers interaction. Things are much better now.

Abstractions require you to learn the framework's interface at the cost of not understanding what's going on below it.

Frameworks can provide code organization and web components, but web components are becoming first class web citizens.

# Web Components
- HTML Templates - content parsed and rendered by browser
- HTML Imports - can import HTML, CSS, and JS
- Custom Elements

# Summary
This can all be combined purely through using the surfaces provided by the browser:
- Attributes
- Events
- DOM Structure

Orthogonal components can be created and used in tandem without requiring a third-party framework.

# Missing Pieces
- CSS Variables/Shadow DOM
- Better Compilers

https://www.polymer-project.org
