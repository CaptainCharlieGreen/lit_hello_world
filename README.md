# To Run

1) Install lit (TODO: link to full docs)

2) Clone this repository
```bash
  $ git clone git@github.com:CaptainCharlieGreen/lit_hello_world.git
```
2) Run lit build in the cloned directory:
```bash
  $ lit build ./HelloWorld.lit
```
4) Run lit deploy on the built .sys file:
```bash
  $ lit deploy ./HelloWorld.sys
```
5) Navigate to localhost:3000 in your browser, or use curl:
```bash
  $ curl localhost:3000
```
# What's going on here?  The Basics

Lit is all about "events", "functions", and "services".  Its sole purpose is to describe what events and functions exist in your system and how those events are handled by those functions.

An "event" is a single piece of serialized data that is passed into your system.  Events come from "sources", and in this example we're including "Http", which is the event source for http requests provided by lit's standard library.  Including Http tells lit that the HelloWorld service accepts http events, or in more familiar terms, that the HelloWorld service is a web server.

A "function" is a single computational unit within your system, and it represents the actual infrastructure that gets deployed (TODO: link to full docs).  Functions accept events and execute code, and "services" are groupings of functions that control access to these infrastructure components.

## Line by line breakdown
```
service HelloWorld {
```
Here we declare a service HelloWorld.  All functions must reside within a service.
### 
```
include "Http"
```
Including Http lets us recieve Http events and tells lit this is a web server
### 
```
Http { method: "get", path: "\*" } ->
```
This is an "event description", and its semantics are determined by the Http event source.  The gist here is we're describing what type of Http event should be sent to the following function.  This can be translated as "All Http get requests should be sent to the following function".
### 
```
helloWorld ():any ->
```
This is a function signature, complete with a function name, input type within the parens (in this case, no input type), and output type after the colon.  Types are not implemented yet in lit, so this function returns the any type while in the future it will return "string".
### 
```
"./helloWorld.js"
```
This is the final part of a function definition--the artifact.  This is the code that will be run in response to the http event declared above.  For now, assume that this .js file will be run by NodeJs...somewhere...more on code execution in (TODO: link to full docs).
