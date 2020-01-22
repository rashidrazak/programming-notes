# Sinon.js

Home Page: https://sinonjs.org/

#### Description
Sinon.js is a standalone test spies, stubs and mocks for JavaScript that works with any unit testing framework.

We usually don't want anything external such as database calls to influence the outcome of the tests.

Spies, stubs and mocks are test doubles. Test doubles can replace troublesome parts of the code and make tests easier to write.

## Spies

Spies record information about function calls, including:
- number of time called
- arguments
- return value
- `this` value
- exceptions thrown (if any)

There are 2 types of spies:
- Anonymous functions
- Ones that wrap methods in our code

### Spies -  Case 1: Anonymous Function

```javascript
function testMe(callback) {
  callback();
}
```

```javascript
describe('testMe', function() {
  it('should call the callback', function() {
    let callbackSpy = sinon.spy();
    testMe(callbackSpy);

    expect(callbackSpy).to.have.been.calledOnce;
  });
});
```

### Spies - Case 2: Wrap an existing method

```javascript
const   user = {
  // ...
  setName: function(name) {
    this.name = name
  }
};
```

```javascript
describe('setName function', function() {
  it('should be called with name', function() {
    let setNameSpy = sinon.spy(user, 'setName');
    user.setName('Rashid Razak');

    expect(setSpyName).to.have.been.calledOnce;
    expect(setSpyName).to.have.been.calledWith('Rashid Razak');

    // Important: Remove the spy at the end to prevent future errors
    setNameSpy.restore();
  });
});
```

## Assertion Styles

```javascript
const sinon = require('sinon');

// Base Sinon assertions
sinon.assertCalledWith(mySpy, 'foo');

// Chai's 'should' and 'expect' interfaces on spy properties:
const chai = require('chai');
const expect = chai.expect;

// Sinon-Chai's 'should' and 'expect' interfaces:
const sinonChai = require('sinon-chai');
chai.use(sinonChai);

mySpy.should.have.been.calledWith('foo');
expect(mySpy).to.have.been.calledWith('foo');
```

## Stubs
Come with all the functionality of spies, but they replace the target function.
Stubs have methods that can add custom behaviours including:
- returning a specific value
- throwing a  specified exception
- automatically invoking callbacks with provided arguments
- defining behaviour on the nth call to stub

Common  use cases for stubs:
- Replacing AJAX calls to prevent database calls
- Triggering different code paths depending on function output
- Testing output when a particular exception is thrown

### Stubs - Case 1: AJAX Call

```javascript
function saveUser(user, callback) {
  jQuery.post('/users', {
    first: user.firstname,
    last: user.lastname
  }, callback);
}
```

```javascript
describe('saveUser', function() {
  it('should call callback after saving', function() {
    // Prevent from sending the post request
    let post = sinon.stub(jQuery, 'post');

    // Make the stub call the 1st callback it receives
    post.yields();

    // Use spy as the callback
    let callbackSpy = sinon.spy();
    let testUserr = {
      firstname: 'Rashid',
      lastname: 'Razak'
    };

    saveUser(testUser, callbackSpy);
    expect(callbackSpy).to.have.been.calledOnce;
    post.restore();
  })
})
```

### Stubs - Case 2: Another AJAX Call

```javascript
function saveUser(user, callback) {
  jQuery.post('/users', {
    first: user.firstname,
    last: user.lastname
  }, callback);
}
```

```javascript
describe('saveUser', function() {
  it('should send correct parameters to the expected URL', function() {
    // Stub $.post as before
    let post = sinon.stub(jQuery, 'post');
    let expectedUrl = '/users';
    let expectedParams = {
      first: 'Expected first name',
      last: 'Expected last name'
    };

    let testUser = {
      firstname: expectedParams.first,
      lastname: expectedParams.last
    };

    saveUser(testUser, function() {}); // We don't care about the callback
    expect(post).to.be.calledWith(expectedUrl, expectedParams);

    post.restore();
  });
});
```

## Mocks

Mocks are similar to stubs, but can be used to replace whole objects and alter their behaviour.

They are mostly used when you need to stub out more than one function from a single object. If you only need to replace a  single function, a stub is easier to use.

**Beware!**
Mocks make it easy to make your tests overly specific and 'brittle'.

Unlike spies and stubs, mocks have built-in assertions. You have to define your expectations up front and call the verification function at the end of the test.

### Mocks - Case 1: Verifying Multiple Behaviours

```javascript
function setupNewUser(info, callback) {
  const user = {
    name: info.name
  };

  try {
    Database.save(user, callback);
  } catch (error) {
    callback(error);
  }
}
```

```javascript
describe('setupNewUser', function() {
  it('should pass object with correct values to save only once', function() {
    let info = { name: 'test' };
    let expectedUser = {
      name: info.name,
      nameLowerCase: info.name.toLowerCase()
    };

    let database = sinon.mock(Database);

    // Expectations can check for multiple conditions at once
    database.expects('save').once().withArgs(expectedUser)

    setupNewUser(info, function() {})
    
    // Verify at the end
    database.verify();
    database.restore();
  })
})
```

## Sinon Best Practices
- Use `sinon-test` for automatic sandbox setup and teardown

How? Instead of using this:
```javascript
describe('testMe function', function() {
  it('should do something', function() {
    let spy = this.spy(testMe);
    testMe(1);

    expect(spy).to.be.calledWith(1);
    spy.restore();
  });
});
```

use this instead:
```javascript
const sinonTest = require('sinon-test');
sinon.test = sinonTest.configureTest(sinon);

describe('testMe function', function() {
  it('should do something', sinon.test(function() {
    let spy = this.spy(testMe);
    testMe(1);

    expect(spy).to.be.calledWith(1);
  })); // Auto cleanup. No need to restore
});
```

### References
1. Youtube Video: https://www.youtube.com/watch?v=Qlmv7nox5pM
2. Sitepoint: https://www.sitepoint.com/sinon-tutorial-javascript-testing-mocks-spies-stubs/
3. SemaphoreCI: https://semaphoreci.com/community/tutorials/best-practices-for-spies-stubs-and-mocks-in-sinon-js

