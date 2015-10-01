# pipeliner
Merge sync and async code in a pipeline

Example of use:

```
var Pipeline = require('pipe');

var pipe = new Pipeline();

//Extended version.
pipe.get('/path/to/some/file')
    .res(function (fileContent) {
      //If the process is sync you must return something.
      return doSomthingSync(filecontent);
    })
    .pipe(function (returnedBefore, next) {
      //If something is async, you have a next method
      getSomthinAsync(function (data) {
        next(data);
      });
    })
    .pipe(function (dataInTheNext) {
      console.log(dataInTheNext);
    });
    
//Functional and verbose version

pipe.get('/path/to/some/file')
    .res(parseFile)
    .pipe(asyncMethod)
    .pipe(logResult);
    
````
