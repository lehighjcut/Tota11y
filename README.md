# An accessibility visualization toolkit.

Drag this link to your browser's bookmarks bar.

<a class="bookmarklet" href="javascript:(function(){var%20tota11y=document.createElement('SCRIPT');tota11y.type='text/javascript';tota11y.src='https://khan.github.io/tota11y/dist/tota11y.min.js';document.getElementsByTagName('head')[0].appendChild(tota11y);})();" onclick="javascript:return false;">tota11y</a>

This is a fork of the original [Tota11y from Khan Academy](http://khan.github.io/tota11y/), by Babylon Health. Inspired by [why Khan Academy built tota11y](http://engineering.khanacademy.org/posts/tota11y.htm), some of the functionality has been updated or tweaked to reflect the needs of Babylon's web developers.

## New Features

### UI changes
- When hovering over a tota11y label, max its z-index in case it is obscured by a nearby label in busy pages.
- Make the menu responsive when screen is zoomed to 200%
- Split out modules into most-common one for content editors, and 'developers' (e.g. those with control over HTML blocks and form fields)
- Add links to Babylon DNA guidance where applicable
- redesigned UI to be white background, easier to see against cookie banners etc

### Screenreader wand

- change the name of screenreader wand, which over-promises (screen readers given other info on form fields, e.g. required)
- added exposure of value attribute on input type=submit fields (as that is what gets exposed and wasn't being reported). 
- Add value of aria-describedby attributes as that is also passed to AT, especially as hints/ instructions on form fields.

### Contrast checker

- stop contrast checker grumbling about transparent (therefore, invisible) text, eg on Amazon, Guardian).  
- don't check text 'visually hidden' using the common clip pattern which we use in Babylon. (Naive test).
- Correct calculation of contrast ratio in the contrast module to take account of boldness of text and not just rely on font-size. (Thanks Mozilla dev tools!). Added MPL license.

### Alt text checker

Tweaked img/alt module to ask users to check accuracy of alt text (rather than perhaps falsely-reassure that presence of alt text is actually useful or related to the image)

### Empty elements plugin added

Add tests for empty nav, header, main, aside, footer, figcaption elements These could be announced to screen reader users (but will be empty) and justifiably make people  grumpy.

### Title attributes plugin added

New Titles module to show missing titles on iframes (error), and warnings for superfluous titles on other things erroneously put there to placate the false idols of Search Engine Optimists (see The Trials and Tribulations of the Title Attribute)

### Landmarks and roles plugin added

New module to expose HTML5 landmarks (footer, header etc) and  ARIA roles that have been explicitly set (but not those that are implicit, because that's not as useful for diagnosing coder errors)

## Installation

`npm install @khanacademy/tota11y`

Include it right before `</body>` like so:

```html
<script src="tota11y.min.js"></script>
```

## Development

Want to contribute to tota11y? Awesome! Run the following in your terminal:

```bash
git clone https://github.com/Khan/tota11y.git
cd tota11y/
npm install
```

## Architecture Overview

Most of the functionality in tota11y comes from its **plugins**. Each plugin
gets its own directory in [`plugins/`](https://github.com/Khan/tota11y/tree/master/plugins) and maintains its own JavaScript, CSS,
and even handlebars. [Here's what the simple LandmarksPlugin looks like](https://github.com/Khan/tota11y/blob/master/plugins/landmarks/index.js).

[`plugins/shared/`](https://github.com/Khan/tota11y/tree/master/plugins/shared) contains a variety of shared utilities for the plugins, namely the [info-panel](https://github.com/Khan/tota11y/tree/master/plugins/shared/info-panel) and [annotate](https://github.com/Khan/tota11y/tree/master/plugins/shared/annotate) modules, which are used to report accessibility violations on the screen.

[`index.js`](https://github.com/Khan/tota11y/blob/master/index.js) brings it all together.

tota11y uses a variety of technologies, including [jQuery](https://jquery.com/), [webpack](https://webpack.github.io/), [babel](https://babeljs.io/), and [JSX](https://facebook.github.io/jsx/). **There's no need to know all (or any!) of these to contribute to tota11y, but we hope tota11y is a good place to learn something new and interesting.**


## Building

To create a development build as the test server uses:

```bash
npm run build:dev
```

To create a production build, with minified and unminified output:

```bash
npm run build:prod
```

## Releasing

Currently, the following steps must be made to release a new version of tota11y:

1. Update `package.json` with the version number to be released.
1. Commit the release details to the CHANGELOG.md.
   This should be list of the unique pull requests and commits that contributed to the release (see the CHANGLOG.md file for previous examples).
1. Draft a new release for the version.
   The tag name and name of the release should be of the form `v1.2.3` where `1.2.3` is the version from `package.json`.
1. Login to `npm` with the Khan Academy credentials.
   This requires someone with appropriate privileges.
1. Run `npm publish`.
   This step will run tests and pre-publish checks, then perform a production build and publish the new package to NPM.
   
## Community Examples
Want to integrate tota11y into your site, but don't know where to start? Here are some examples from the tota11y community to inspire you:
* [azemetre/webpack-react-typescript-project](https://github.com/azemetre/tota11y-webpack-react-typescript-example) shows how to integrate tota11y into a webpack build for a React + TypeScript project.

## Special thanks

Many of tota11y's features come straight from [Google Chrome's Accessibility Developer Tools](https://github.com/GoogleChrome/accessibility-developer-tools). 

## License

[MIT License](LICENSE.txt)
