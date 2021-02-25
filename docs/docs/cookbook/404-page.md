---
title: 404 Page
---

> You are reading the documentation for version 2 of FoalTS. Instructions for upgrading to this version are available [here](../upgrade-to-v2/README.md). The old documentation can be found [here](https://github.com/FoalTS/foal/tree/v1.x/docs).

Here's a way to implement custom 404 pages.

```typescript
import { Get, HttpResponseNotFound, HttpResponseOK } from '@foal/core';

class ViewController {
  @Get('/home')
  home() {
    return new HttpResponseOK('You are on the home page!');
  }
}

class AppController {
  subControllers = [ ViewController ];

  @Get('*')
  notFound() {
    return new HttpResponseNotFound('The page you are looking for does not exist.');
  }
}
```

In case you want to intercept all HTTP verbs (POST, PUT, etc), you can also use the `@All` decorator for this.

> *This feature is available from version 2.1 onwards.*

```typescript
import { All, HttpResponseNotFound } from '@foal/core';

class AppController {
  subControllers = [ ViewController ];

  @All('*')
  notFound() {
    return new HttpResponseNotFound('The route you are looking for does not exist.');
  }
}
```