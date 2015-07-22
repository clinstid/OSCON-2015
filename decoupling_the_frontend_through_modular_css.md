# Decoupling the Front-end Through Modular CSS
Using CSS selection that mixes element type, class, id, etc. can create a fragile coupling of HTML, CSS, and JS. Modular CSS based on classes can alleviate this issue.

# OOCSS (Object Oriented CSS)
Use objects with classes to define repeated common blocks. A good example is a media object that contains an image and some text. The object is a media object that has child elements. Each part of the object should have its own class name that represents the element of the object.

Example:
- `media`: The full object
    - `media__img`: The image in the media object
    - `media__text`: The text in the media object

Using the classes, we can apply style to elements within the object without needing to know what type of element it is. That allows us to change the element type within HTML and still have the same styling applied. The same rule applies when using JS to apply styles.

## Naming
Most important naming rule is to pick a style and stay consistent. A good option is BEM - Block Element Modifier:

`block__element--modifier`

`block` is the object type, `element` is the name of a child element of the object, and `modifier` is an alternate style on the object. A double underscore separates the `block` and `element` names and a double hyphen separates the `element` and `modifier` names.

- Structure vs. Skin
- Container vs. Content

Downside to OOCSS is that you end up with a ton of classes. The upside is that the coupling between HTML and CSS is broken and replaced with a coupling of HTML and style.

# Presentational Arguments
- Classes have no meaning to browsers.
- Classes are semantic to developers.
