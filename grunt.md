Grunt Cheatsheet
================
##Requirements
* Node.js
* Npm

##Basic Setup
1. install grunt-cli: ```npm install -g grunt-cli```
2. Change to project folder on command line
3. Create a ```package.json``` file: ```npm init```. Follow prompts to name project, version and other info.
4. Install grunt plugins: ```npm install grunt-contrib-uglify --save-dev```. The ```--save-dev``` part makes sure  Npm adds the package to the ```Package.json``` file.
5. Create ```Gruntfile.js``` file. This file describes the tasks you want Grunt to perform.

##The Grunt File
A Grunt file is composed of 3 main sections:

1. **Task Configuration** The ```grunt.initConfig()``` method sets up the options for the various tasks you want to perform. It sets up settings for the Grunt plugins to tell those plugins how they should work and what they should do.
2. **Loading plugins** You need to tell Grunt which plugins it should lod using a series of ```grunt.loadNpmTasks()``` calls. For example: ```grunt.loadNpmTasks('grunt-contrib-uglify');```
3. **Task registration** At the end of the file you register the different tasks you want Grunt to perform. For example: ```grunt.registerTask('default', ['uglify:dev', 'sass:dev', 'jshint']);```. You can define different named sets of tasks which will run when invoked using a specified name. For example you can create a set of tasks named ```dev``` which might include tasks you want to run while developing the site, such as compiling Sass into CSS or running your JavaScript through JSHint. You could then run just those tasks from the command line like this ```grunt dev```

###Gruntfile.js Skeleton
```
module.exports = function(grunt) {

  // Project configuration.
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    
    // add task configurations here
    
  });

  // Load plugins
  grunt.loadNpmTasks();
  
  // Register task(s).
  grunt.registerTask('default', []);
  
};
```

###Example Gruntfile.js
```
module.exports = function(grunt) {

  // Project configuration.
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    uglify: {
      options: {
        banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n'
      },
      build: {
        src: 'src/script.js',
        dest: 'js/script.min.js'
      }
    }
  });

  // Load the plugin that provides the "uglify" task.
  grunt.loadNpmTasks('grunt-contrib-uglify');

  // Default task(s).
  grunt.registerTask('default', ['uglify']);

};
```
##Running Grunt
To run the default set of tasks, you only need to type this on the command line:

```
grunt
```
Note: you need to be in the directory where the gruntfile.js is located.

You can also run other sets of tasks that you have named. For example to run the "dev" tasks:

```
grunt dev
```
You can also run individual tasks that you've defined in the ```grunt.initConfig()``` method. For example, if you've added a JSHint task, you could run it like this:

```
grunt jshint
```
You can set up Grunt plugins to behave differently depending on which group of tasks you run. For example, during development you don't want to minify your JavaScript code, so you would turn off the uglify plugin during dev. However you'd turn it on for distribution. You could uglify your JS using the distribution (dist) version like this:

```
grunt uglify:dist
```
##Plugin Examples
###JSHint
```npm install grunt-jshint --save-dev```
#####grunt.initconfig()
```
jshint: {
   all: ['src/js/*.js']
}
```
#####load plugin
```
grunt.loadNpmTasks('grunt-contrib-jshint');
```
#####register task
```
grunt.registerTask('dev', ['jshint']);
```
###Uglify
```npm install grunt-jshint --save-dev```
#####grunt.initconfig()
```
uglify: {
      options: {
        banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n'
      },
      dist: {
        files: {
          'js/<%= pkg.name %>.min.js' : 'src/js/*.js'
        }
      },
      dev: {
        options: {
          compress: false,
          beautify: true,
          mangle: false
        },
        files: {
          'js/<%= pkg.name %>.min.js' : 'src/js/*.js'
        }
      }
    }
```
#####load plugin
```
grunt.loadNpmTasks('grunt-contrib-uglify');
```
#####register task
```
grunt.registerTask('dev', ['uglify:dev']);
grunt.registerTask('dist', ['uglify:dist']);
```
###Grunt Sass
```npm install grunt-sass --save-dev```
#####grunt.initconfig()
```
sass: {
      options: {
        banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n'
      },
      dist: {
        options: {
          outputStyle: 'compressed'
        },
        files: {
          'css/styles.min.css' : 'src/css/styles.scss'
        }
      },
      dev: {
        options: {
          outputStyle: 'expanded'
        },
        files: {
          'css/styles.min.css' : 'src/css/styles.scss'
        }
      }
    }
```
#####load plugin
```
grunt.loadNpmTasks('grunt-sass');
```
#####register task
```
grunt.registerTask('default', ['sass:dev']);
grunt.registerTask('dist', ['sass:dist']);
```
###Other Plugins
* HTMLHint
	* ensure unique ID's
	* Ensure valid attributes
	* Tags are correct and valid
 





