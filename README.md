# pyNut
---
**Minimalist build system.**

This is a generic **minimalist build system**, this was made to write web. app. without hassles.

This is a simplified port of [nut](https://github.com/grz0zrg/nut), a more advanced build system made with the Anubis language.

It is basically a simple pre-processor which is capable of concatenating files with an include directive pattern (not recursively) then execute programs to produce a production file like minification, optimizer etc.

This build system has no live check & "build on file change" features unlike Nut but you can add thoses easily under Linux or similar systems with inotify tool.

You only need to pass app files or directories as argument, pyNut will scan one or multiple app files which start with "app_" as filename, they are the entry point of your applications, in these files you can then use directives such as include as follow: `/*#include [FILENAME]*/` pyNut will read the entry point file sequentially, include the content of `[FILENAME]` if the directive is encountered and output a single file application in a dist folder, CSS and JS is automatically detected from the file extension and a program such as a minifier will be called and output a production ready file as well.

It is essential to start pyNut in the application root directory, a folder named `dist` should be there as well.

Base example for web. applications with JS and CSS (basic setup):
 * `uglifyjs` and `csso` should be installed with Node/NPM `npm install uglifyjs csso`
 * The app. folder should contain a `js` and `css` folder
 * `js` folder should contain a file named `app_[APP_NAME].js` where `[APP_NAME]` is your application name
 * `css` folder should contain a file named `app_[APP_NAME].css` where `[APP_NAME]` is your application name
 * Call Nut in the app. root directory with `python pynut.py [APP_NAME].js [APP_NAME].css`
 * The debug and production ready files will be available in the `dist` folder as `[APP_NAME].js` `[APP_NAME].css` `[APP_NAME].min.js` `[APP_NAME].min.css`

You can use a folder directly as argument, this will execute the merging process + prod. process for each files in the directory.

Features:
 - Produce debug and production ready files, minified & optimized CSS and JS output in a `dist` folder
 - Not restricted to a single build
 - Can produce build files for a whole directory if specified (may be useful in case of JS workers)
 - Parse `/*#include [FILENAME]*/` directives to provide **KISS** modularity
 - Generic & Customizable (see pynut.py) you can customize the include pattern, tools to execute for production and the entry point prefix
 - Minimalist :)

It is not restricted to a single output, just create as many entry point files as wanted and pass a list of output files as argument.

Usage: `Usage: python pynut.py [APP_NAME].js [APP_NAME].css`
