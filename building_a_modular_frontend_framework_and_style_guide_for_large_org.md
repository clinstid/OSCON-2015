# Building a Modular Front End Framework and Style Guide for a Large Organization
How do you keep design and code consistent with a large team?

Create an open, transparent standard and UI framework that makes it easy for developers to adopt, implement, and maintain.

# Design Manual
Good example is the UK Government Design Manual - https://www.gov.uk/service-manual

Design manual developed in public with open collaboration. While it's the not the most efficient method of developing the style guide, it includes everyone in the conversation which gives everyone a feeling of ownership and thus is more likely to be followed voluntarily.

# Framework
1. Collection of modular HTML/CSS/JS components
1. Build process
1. ?

## Modular
Logical division of modules into separate repos/projects. Pull in only what you need. Update only what you need to simplify testing.

## Build Process
- Common build process using tools like NPM and Bower to manage dependencies and grunt to run build tasks.
- Modular components allow for smaller impact radius for new features and phased adoption.

# Updates
The design manual is built using the framework, so there's an interdependency that forces documentation and framework updates to happen in tandem.
