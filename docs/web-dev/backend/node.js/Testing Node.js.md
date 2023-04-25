- have descriptive test names,

- bad: `isAgeValid()`, good: `age is between 15 and 100`

- you're going to be reading this a lot

Tests -> Tools -> Patterns -> Design -> Tests -> ...

## Mocha

- To test a feature, each `describe` should have a `before` which creates the scenario.

- each `it` specified the behaviour

- don't use arrow functions

- if you want to change mocha settings like `this.timeout(2500)`

- first `describe` block is the acceptance tests (integrity), should always be right `will work if ...`

- second `describe` block: should try to break things

- `won't work if ...`

- don't change things from another block

  

### mocha tools

`describe.only( ... )`

- will only run that one describe

- also works for `it.only()`, USE THIS if that one test case fails

- `it.skip()` will skip that test case

- Print the results of the tests `mocha --reporter doc > report.html`

  

- can have nested directory sturcture, just have the `npm test` script in package.json:

```json

scripts: {

test: "mocha ./test/**/*.spec.js"

}

```

  

### Mocha and Asynchronous Code

```js

// expects a callback

it('...', function(done) {

done(); // mocha will continue to run the next test

}

```

- can also use the `mocha-generators` module when dealing with promises

  

## Sinon

- `var func = sinon.spy()`

- gives a fake function that can track lots of information

- can track how many times it was called, lots more

- for each, see what the args were

- watch an existing function

- `sinon.stub(obj, 'function').returns(true)`: replace a function, control it to do what we want

- kills the function

- `sinon.stub(obj, 'functionName').throws()`

  

### Sinon and event triggers

```js

var spy = sinon.spy();

eventEmitter.on("validated", spy);

assert(spy.called);

```

obviously, this isn't fun, avoid using event triggers, use promises, or `async`

  

### Sinon and database

`sinon.stub(db, "find").yields(null, {id: 1});`

  

### Repository Design Pattern

- shouldn't use it over a large code base

  

####Mocks

```js

var mock = sinon.mock(res);

mock.expects('render').twice().withExactArgs('index');

```

- Singletons are not friendly to mocking

`exports.aPropertyName = {};` is the only line in the file

  

#### Mocking HTTP

Problem 1: Https is a built-in node.js module

Solution

```js

beforeEach(function() {

// we only want to stub the request function of https

this.request = sinon.stub(https, 'request');

});

```

  

### Nock module (HTTP mocking)

- mock API calls from code to an external API

- mocking can be destructive, can cause more problems than it's worth

- don't mock something you don't own

- otherwise, you're going to have to do some sleuthing and look at module code

  

Problem 2: https uses a stream, we need to mock a stream

```js

var PassThrough = require('stream').PassThrough;

var response = new PassThrough();

response.write(JSON.stringify({some: "json"});

response.end();

```

  

### NeDB

- like SQLite for Node

- uses MongoDB syntax

  

## Learning Paths

### Fundamentals Track

- basic literacy, fundamental ideas (OOP, GPU, CPU, async)

- widely applicable

- rarely become obsolete

- can still be complex, not necessarily beginner

- can transfer to others

  

### Information

- specific knowledge

- Fundamental: what is an int, Information: in C++

- obsolete very quickly

  

### Skills

- use knowledge to get things done

- gets you income

  

Competence

- when you have lots of all three

- good enough

  

### Innovation (expertise)

- After competence

- tracks after the first three

- creates the fundamentals, information, skills

- hard work, usually by accident, they're passionate about a technology and end up an expert

  

Choosing a platform over a language

- OS platforms (Android)

- Application Platforms (Facebook, Drupal)

- API Platforms (Twitter, Amazon, Google)

- Delivery platforms (AWS, Azure, Heroku)

  

Where do you start?

- books, courses, have curation

  

Certificates

- valuable if employees want them

- open source contributions