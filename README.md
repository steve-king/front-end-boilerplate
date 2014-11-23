Front-end Boilerplate
=====================

A Node, Grunt and Bower powered, quick start boilerplate for fully optimised front-end builds.

## Usage

Assuming you already have Node, Grunt and Bower installed: 
- clone the project, cd to directory
- run `npm install` 
- then `bower install`
- then `grunt init` - to initial compile
- then `grunt` - to run watch/serve

## Features:

- grunt-sass for lightning fast SASS compilation (much quicker than grunt-contrib-sass)
- Bower for JS library source control
- wiredep for automatically linking to bower JS dependencies in the footer, in correct order. Runs on all HTML files found in root with `<!-- bower:js -->` tags 
- jshint with "jshint-stylish" output
- grunticon and svgmin for automated icon CSS output - runs on any SVG files found in dev/images/svg-src by default.
- watch triggers are broken up by file type, and are optimised for speed with grunt-newer.
- Nodemon runs a Node server in parallel with the watch task to serve up files on localhost. 
- Server.js parses HTML files in the dev folder as EJS templates, allowing you to use EJS `<% include file.html %>` tags during dev, and then render out into flat HTML during build.
- grunt-usemin will concatenate and minify/uglify files linked to from within `<!-- build -->` tags in your HTML and replace refs to the minified assets in build folder.
- imagemin compressions
- Twitter Bootstrap for quick prototyping, easily customisable to import only the stuff you need



### Bootstrap
Twitter bootstrap-sass-official is the only bower dependency included, and currently configured import CSS only. If you really want to get tall the JS too, remove the "overrides" object for bootstrap in `bower.json` before you run `bower install` 

To customise the SCSS parts of bootsrap that are imported, edit `dev/scss/bootstrap-custom.scss` and uncomment components as needed. At the moment, only mixins, normalize (css reset), grid, responsive utilities, and helper classes are imported. The variables needed to adjust the grid have been copied into `dev/scss/variables.scss` from  `bower_components/bootstrap-sass-official/assets/stylesheets/bootsrap/variables.scss` - you will need to grab any extra vars for any other components you import from this file.

### Gruntfile.js
You can change the locaton of the dev and build folders in the "paths" object near the top of the Gruntfile. By default these are set to `dev` and `build`. Note: you'll also need to update the dev folder location in the `.bowerrc` file.

Grunt tasks:

- `grunt init` - run this the first time you check out the project. Compiles SASS, wires up any bower dependencies and builds your icons for the first time
- `grunt` - (default task) runs a watch and Node server task concurrently. Dev folder can be browsed at http://localhost:3000
- `grunt serve` - Will serve up the build folder for you to preview
- `grunt serve:dev` - Serves up the dev folder, without running "watch"
- `grunt build` - Will run the build task into the specified build folder
- `grunt svg_icons` - Run the SVG icon task chain on it's own

### Server.js
You will need to add a new route here for any new HTML templates you add to your root folder.
- TODO: set up some sort of dynamic routing
- TODO: Pull in a JSON file of template variables e.g "global.json" and "template-name.json". These will have to be accessible to the grunt-ejs-render task aswell (below)

### EJS template rendering
Currently, grunt-ejs-render does not allow `files : { expand: true }` at the moment, so you will also have to add new HTML templates to this task definition in the Gruntfile
- TODO: Link to JSON files for dynamic content...
