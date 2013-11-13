!SLIDE ============================

# Bienvenu dans le monde merveilleux du web

![](img/arc-en-ciel.gif)

!SLIDE bullets ============================

#Js Tools

*Où comment optimiser nos devs*

!SLIDE bullets ============================

#Sommaire

* Node.js / NPM
* Grunt
* Bower
* Karma

!SLIDE bullets ============================

<div style="background-color:black; display:inline-block">
![](img/nodejs.png)
</div>

!SLIDE bullets ============================

##Node.js

* Site : [http://nodejs.org/](http://nodejs.org/)
* But : Exécuter du code Javascript
* Java : JVM

!SLIDE bullets ============================

![](img/npm.png)

!SLIDE bullets ============================

##NPM : Node Packaged Modules

* Site : [https://npmjs.org/](https://npmjs.org/)
* But : Télécharger les dépendances "static" (des outils)
* Compris par défaut dans Node.js
* Java : Maven

!SLIDE bullets ============================

![](img/grunt.png)

!SLIDE bullets ============================

##Grunt

* Site : [http://gruntjs.com/](http://gruntjs.com/)
* But : Runner de tasks
* Installation : npm install -g grunt-cli
* Java : Maven/Ant

!SLIDE bullets ============================

##Configuration

* grunt init
* ou utiliser un boilerplate

!SLIDE smaller ============================

```javascript
module.exports = function ( grunt ) {
  
  grunt.loadNpmTasks('grunt-contrib-clean');//clean directory
  grunt.loadNpmTasks('grunt-contrib-copy');//copy content
  grunt.loadNpmTasks('grunt-contrib-concat');//concat files
  grunt.loadNpmTasks('grunt-recess');//build css
  grunt.loadNpmTasks('grunt-contrib-uglify');//min js
  grunt.loadNpmTasks('grunt-contrib-watch');//reload on change
  grunt.loadNpmTasks('grunt-karma');//run tests
  grunt.loadNpmTasks('grunt-contrib-jshint');//check syntaxe
  grunt.loadNpmTasks('grunt-contrib-connect');//server
  
  var gruntConfig = require( './config/gruntConfig.js' );

  var taskConfig = {

    pkg: grunt.file.readJSON("package.json"),
    meta: {
      banner: 
        '/**\n' +
        ' * <%= pkg.name %> - v<%= pkg.version %>\n' +
        ' * <%= pkg.homepage %>\n' +
        ' *\n' +
        ' * Copyright (c) <%= grunt.template.today("yyyy") %> <%= pkg.author %>\n' +
        ' * Licensed <%= pkg.licenses.type %> <<%= pkg.licenses.url %>>\n' +
        ' */\n'
    },

    clean: [ 
      '<%= build_dir %>', 
      '<%= compile_dir %>'
    ],
...
```

!SLIDE smaller ============================

```javascript
  grunt.initConfig( grunt.util._.extend( taskConfig, gruntConfig ) );
  grunt.registerTask( 'build', [ 'clean', 'copy:build', 'index:build'] );
  grunt.registerTask( 'compile', [ 
    'jshint', 'karma:compile:start', 'build', 'recess:compile', 
    'concat:compile_js', 'uglify:compile', 'copy:compile', 'index:compile'] );
  grunt.registerTask( 'dev', [ 'connect','jshint', 'karma:build:start', 'watch' ] );
  grunt.registerTask( 'default', [ 'build'] );
```

!SLIDE smaller ============================

```javascript
module.exports = {
  
  build_dir: 'build',
  compile_dir: 'bin',

  app_files: {
    first: [],
    js: [ 'app/src/**/*.js' ],
    html: [ 'app/index.tpl.html' ],
    stylesheet: ['app/stylesheet/**/*.less'],
    assets: ['app/assets/**/*'],
    less: 'app/stylesheet/main.less',
  },
...
```

!SLIDE bullets ============================

##Utilisation

* npm install (1ere utilisation)
* grunt task-name

!SLIDE bullets ============================

![](img/bower.png)

!SLIDE bullets ============================

##Bower

* Site : [https://github.com/bower/bower](https://github.com/bower/bower)
* But : Télécharger les dépendances "dynamic" (du projet)
* Installation : npm install -g bower
* Java : Maven

!SLIDE bullets ============================

##Configuration

* bower init
* ou utiliser un boilerplate

!SLIDE ============================

```javascript
{
  "name": "Project name",
  "version": "0.0.1",
  "ignore": [
    ".jshintrc",
    "**/*.txt"
  ],
  "dependencies": {
    "underscore": "~1.5.2"
  },
  "devDependencies": {}
}
```

!SLIDE bullets ============================

##Utilisation

* bower install (1ere utilisation)
* bower list (show update)
* bower install package#version (new package)

!SLIDE bullets ============================

![](img/karma.png)

!SLIDE bullets ============================

##Karma

* Site : [http://karma-runner.github.io/](http://karma-runner.github.io/)
* But : Exécuter des libs qui vont exécuter des tests
* Installation : npm install -g karma
* Java : <s>au dessus de</s> JUnit

!SLIDE bullets ============================

##Configuration

* karma init
* ou utiliser un boilerplate

!SLIDE smaller ============================

```javascript
module.exports = function(config) {
  config.set({
    basePath: '',
    // frameworks to use
    frameworks: ['jasmine', 'requirejs'],
    // list of files / patterns to load in the browser
    files: [
      {pattern: "app/src/**/*.js", included:false},
      {pattern: "test/**/*.spec.js", included:false},
      "test/main.test.js"
    ],
...
    port: 9876,
...
    autoWatch: true,
    // Start these browsers, currently available:
    // - Chrome
    // - ChromeCanary
    // - Firefox
    // - Opera (has to be installed with `npm install karma-opera-launcher`)
    // - Safari (only Mac; has to be installed with `npm install karma-safari-launcher`)
    // - PhantomJS
    // - IE (only Windows; has to be installed with `npm install karma-ie-launcher`)
    browsers: ['PhantomJS'],
...
  });
};
```

!SLIDE smaller ============================

```javascript
var tests = Object.keys(window.__karma__.files).filter(function (file) {
  var regexp = /spec\.js$/;
  return regexp.test(file);
});

requirejs.config({
  // Karma serves files from '/base'
  baseUrl: '/base/app/src',

  // ask Require.js to load these files (all our tests)
  deps: tests,

  // start test run, once Require.js is done
  callback: window.__karma__.start
});
```

!SLIDE smaller ============================

#Tout est en place ?

!SLIDE smaller ============================

```javascript
grunt.registerTask( 'dev', [ 
  'connect',//démarre le serveur
  'jshint',//check la syntaxe
  'karma:build:start',//démarre le serveur de test
  'watch'//modification entraîne...
  ] );
```

```javascript
watch: {
  files: [ 
     '<%= app_files.html %>', 
     '<%= app_files.js %>', 
     '<%= vendor_files.js %>', 
     '<%= app_files.assets %>', 
     '<%= app_files.stylesheet %>', 
     '<%= test_files.js %>' 
  ],
  tasks: [
    'jshint',//check la syntaxe
    'karma:build:run',//exécute les tests
    'build'//"compile html", copie (js, css, assets...)...
  ]
},
```

!SLIDE smaller ============================

#Vous allez voir maintenant avec le dojo !