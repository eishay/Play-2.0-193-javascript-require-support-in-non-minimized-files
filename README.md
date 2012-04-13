Demonstrating the issue described at https://play.lighthouseapp.com/projects/82401/tickets/193-javascript-require-support-in-non-minimized-files "javascript require support in non-minimized files".
The demo runs on Play 2.1-SNAPSHOT 21ba2e879b7912b44f1edf5f9e2ab6cf9fe5e4cb from https://github.com/playframework/Play20.git

The functionality demoed is described at http://www.playframework.org/documentation/2.0/AssetsGoogleClosureCompiler "CommonJS-style dependencies" 

## Fetching the javascripts
The following commands are fetching the test.js javascript file from https://github.com/eishay/Play-2.0-193-javascript-require-support-in-non-minimized-files/blob/master/requireDemo/app/assets/javascript/test.js
The first call is fetching test.js, the second is fetching test.min.js
While in test.min.js closure compiled require("lib") into its modules system, it did not do so with test.js.

```javascript
$ curl http://localhost:9000/assets/javascript/test.js;echo;
// The test

require("lib");

function showSum(first, second) {
    alert(require("lib").sum(first, second));
}

showSum([2,3], 4);
```
```javascript
$ curl http://localhost:9000/assets/javascript/test.min.js;echo;
var module$lib={};function sum$$module$lib(a,b){return a+b}module$lib.sum=sum$$module$lib;if(module$lib.module$exports)module$lib=module$lib.module$exports;var module$test={};module$lib;function showSum$$module$test(first,second){alert(module$lib.sum(first,second))}showSum$$module$test([2,3],4);if(module$test.module$exports)module$test=module$test.module$exports;
```

## Here is a bit prettier test.min.js:

```javascript
var module$lib={
};
function sum$$module$lib(a,b){
	return a+b
}
module$lib.sum=sum$$module$lib;
if(module$lib.module$exports)
	module$lib=module$lib.module$exports;
var module$test={
};
module$lib;
function showSum$$module$test(first,second){
	alert(module$lib.sum(first,second))
}
showSum$$module$test([2,3],4);
if(module$test.module$exports)
	module$test=module$test.module$exports;
```

