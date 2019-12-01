# Asmodee Security Presentation

## Bootstrap

To start viewing or editing the presentation, one need:

* nodejs
* npm

On mac you can install both with:

~~~sh
brew install node
~~~

Then you need to get the libraries:

~~~sh
npm install
~~~


## Editing the slides

Edit the `slides/security.md` file.
This is a `Github` flavored markdown file.

Each horizontal slides are separated by `---`. Each vertical slides are separated by `--`.
Style is by default 'centered'.

Speaker notes can be added to a slide by adding:

~~~text

Slide content
More slide content

note: blah blah my speaker note are there
but also there, until the end of the slide
~~~

You can change the global style in the `templates/_index.html`.

## Viewing the presentation

Type:

~~~sh
npm start
~~~

This will open a browser windows with the slide views. You can navigate the presentation with the 'Space' key.

### Keyboard access

| N,SPACE| Next slide         |
| P      | Previous slide     |
| ← , H  | Navigate left      |
| → , L  | Navigate right     |
| ↑ , K  | Navigate up        |
| ↓ , J  | Navigate down      |
| Home   | First slide        |
| End    | Last slide         |
| B, .   | Pause              |
| F      | Fullscreen         |
| ESC, O | Slide overview     |
| S	     | Speaker notes view |