# roc-yarn-test

This repo was created to demonstrate that I cannot use `roc` with `yarn`.

### Let's run it with `npm` first:

```
npm install
roc dev
```

### I get:

```
Found a local version of Roc, will use that over the global one. 

ℹ Roc runtime has been initialized.
webpack built d7506b0e9b794fc333e0 in 6969ms
  roc:server Server started on port 3000 (HTTP) and served from / +0ms
  <-- GET /
[BS] Proxying: http://0.0.0.0:3000
[BS] Access URLs:
 ---------------------------------------
       Local: http://localhost:3030
    External: http://10.164.132.130:3030
 ---------------------------------------
          UI: http://localhost:3031
 UI External: http://10.164.132.130:3031
 ---------------------------------------
  --> GET / 200 161ms 16.56kb
  <-- GET /
  --> GET / 200 40ms 16.56kb
```

Everything looks good. Works as expected.

### Let's see what happens when I switch to `yarn`:

```
rm -rf node_modules
yarn install
```

### I get:

```
$ roc dev
  Warning    Roc Extension Failed

  Failed to load Roc package roc-package-web-app-react

  Will ignore extension. Expected it to have a name.
  Occurred in: undefined

  Occurred in roc-package-web-app-react

  Warning    Roc Extension Failed

  Failed to load Roc package roc-package-web-app-react-dev

  Will ignore extension. Expected it to have a name.
  Occurred in: undefined

  Occurred in roc-package-web-app-react-dev

  Warning    Roc Extension Failed

  Failed to load Roc plugin roc-plugin-style-sass

  Will ignore extension. Expected it to have a name.
  Occurred in: undefined

  Occurred in roc-plugin-style-sass

  Warning    Configuration

  There was a mismatch in the application configuration structure, make sure this is correct.
  Did not understand settings.runtime.applicationName
  Did not understand settings.runtime.port
  Did not understand settings.runtime.serve
  Did not understand settings.runtime.favicon
  Did not understand settings.build.reducers
  Did not understand settings.build.routes

  Error    Invalid Command

  Did not understand dev - Did you mean new
```

### This is my global configuration:

```
$ which roc
/Users/wadim/.nvm/versions/node/v6.7.0/bin/roc
$ roc --version
1.0.0-rc.10
```

### Clone this repo to reproduce

This is a fresh new app from the `web-app-react` template.

The only thing I changed in the repo (with respect to the code generated from the template) is:
 - Updated `roc-package-web-app-react` to `1.0.0-beta.9`
 - Updated `roc-package-web-app-react-dev` to `1.0.0-beta.9`
 - Updated `roc-plugin-style-sass` to `1.0.0-beta.4`
 - Added `.babelrc` with `{ "presets": ["es2015", "es2016", "es2017", "stage-0"] }` because it refused to work without it
