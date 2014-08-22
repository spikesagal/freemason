freemason
=========

A simple way to bundle, minify, and attribute JavaScript packages. No configuration required!

Here is an example of a build file (let's name it `build.js`:

```JavaScript
var build = require('freemason').tasks;
build.concatenate('LAB.src.js','jsrequire.src.js');
build.minify();
build.attribute('src/credits.txt');
build.write('dist/jsrequire.min.js');
```

To run the build, just run `node build.js`. That's it! This is all you need to do in order to concatenated a bunch of files, minify/obfuscate the result, put some credits on top, and write it to a file.

Want to write your own tasks? There are only four conventions to keep in mind:

1. `buffer` is used by all tasks implicitly, to store the state of your build.
2. `tasks` contains all the default tasks (currently `concatenate`, `minify`, `attribute`, and `write`).
3. `queueTask` must be used to run a task synchronously, and all calls to `queueTask` must be made within the first execution loop. Don't queue tasks on asynchronous callbacks -- it won't work. Instead, build any asynchronous functionality into the task definition.
4. `taskDone` must be called when the task is complete, in order to move on to the next task.
