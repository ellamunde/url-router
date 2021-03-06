[ ![Download](https://api.bintray.com/packages/mrhabibi/maven/url-router/images/download.svg) ](https://bintray.com/mrhabibi/maven/url-router/_latestVersion)

# URL Router
A wrapper for easily routing URL on Android

## Examples

### Initialization

```
/* 
 * Mapping the schema and host
 */
 
Router.getInstance().preMap("*://<subdomain:[a-z]+>.mysite.com/*", (ctx, result) -> {
    String subdomain = result.variables.get("subdomain");
    if (subdomain.equals("blog")) {
        // Launch intent
        ...
        return null; // Don't continue to path routing below by returning null
    } else {
        return Uri.parse(result.url).getPath(); // Continue to path routing below
    }
});

/* 
 * Mapping the path
 */

/* Simple mapping */

Router.getInstance().map("/about", (ctx, result) -> {
    ...
});

/* Wildcard at the end for any characters until end of url */

Router.getInstance().map("/promo/*", (ctx, result) -> {
    ...
});

/* Wildcard in segment for any character in specific segment */

Router.getInstance().map("/promo/*/discounted", (ctx, result) -> {
    ...
});

/* Get value from parsed queries */

Router.getInstance().map("/register", (ctx, result) -> {
    String referrer = result.queries.get("referrer")
    ...
});

/* Get value from parsed variables in segment of path */

Router.getInstance().map("/transaction/<transaction_id>/view", (ctx, result) -> {
    String transactionId = result.variables.get("transaction_id")
    ...
});

/* Get value from parsed variables in subsegment of segment */

Router.getInstance().map("/product/<product_id:[a-z0-9]+>-*", (ctx, result) -> {
    String productId = result.variables.get("product_id")
    ...
});
```

### Usage

```
Router.getInstance().route(context, url, optionalArgs)
```

### Multiple Instances

```
Router loginUserRouter = new Router();
Router nonloginUserRouter = new Router();
```

### Language

#### Wildcard : `*`
- Can be placed anywhere except query
- Used for replacing any character inside URL
- Regex: `.+` -> Any character more than 1

#### Variable Name : `<variable_name>`
- Can be placed anywhere except query
- Used for getting value inside URL
- Variable name can only use `A-Z`, `a-z`, `0-9`, and `_`
- Default regex: `[^/]+` -> Any character more than 1 except `/`
- Default regex can be changed

#### Variable Name With Specific Pattern : `<variable_name:[a-z0-9]+>`
- Can be placed anywhere except query
- Used for getting value inside URL
- Variable name can only use `A-Z`, `a-z`, `0-9`, and `_`
- Default regex: `[^/]+` -> Any character more than 1 except `/`
- Default regex can be changed
- Variable name and regex separated with `:`
- Specific regex overrides default regex

## Installation

### Gradle

Add this line in your `build.gradle` file:

```
compile 'com.bukalapak:url-router:0.1.0'
```

This library is hosted in the [JCenter repository](https://bintray.com/bukalapak/maven), so you have to ensure that the repository is included:

```
buildscript {
   repositories {
      jcenter()
   }
}
```

## Contributions

Feel free to create issues and pull requests.

## License

```
URL Router library for Android
Copyright (c) 2017 Bukalapak (http://github.com/bukalapak).

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```