# api documentation for  [express-bunyan-logger (v1.3.1)](https://github.com/villadora/express-bunyan-logger#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-express-bunyan-logger.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-express-bunyan-logger) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-express-bunyan-logger.svg)](https://travis-ci.org/npmdoc/node-npmdoc-express-bunyan-logger)
#### a bunyan logger middleware for express

[![NPM](https://nodei.co/npm/express-bunyan-logger.png?downloads=true)](https://www.npmjs.com/package/express-bunyan-logger)

[![apidoc](https://npmdoc.github.io/node-npmdoc-express-bunyan-logger/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-express-bunyan-logger_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-express-bunyan-logger/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-express-bunyan-logger/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-express-bunyan-logger/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "wei.gao",
        "email": "jky239@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/villadora/express-bunyan-logger/issues"
    },
    "contributors": [
        {
            "name": "Wei Gao",
            "email": "jky239@gmail.com"
        },
        {
            "name": "Paris Holley",
            "email": "mail@parisholley.com"
        },
        {
            "name": "Ognian Tschakalov",
            "email": "ognian.tschakalov@ogi-it.com"
        },
        {
            "name": "Simon Wade",
            "email": "simon.wade@gmail.com"
        }
    ],
    "dependencies": {
        "bunyan": "^1.8.1",
        "lodash.has": "^4.5.1",
        "lodash.set": "^4.3.1",
        "node-uuid": "^1.4.7",
        "useragent": "^2.1.9"
    },
    "description": "a bunyan logger middleware for express",
    "devDependencies": {
        "body-parser": "^1.15.2",
        "express": "^4.14.0",
        "jshint": "^2.9.2",
        "mocha": "^3.0.1",
        "supertest": "^2.0.0",
        "through2": "^2.0.1"
    },
    "directories": {},
    "dist": {
        "shasum": "36ee66bbcf580f3085bc6a003f55b8421bbc2460",
        "tarball": "https://registry.npmjs.org/express-bunyan-logger/-/express-bunyan-logger-1.3.1.tgz"
    },
    "gitHead": "629ed821f9fbd64e32a0449ff08281ad5f3aa0ed",
    "homepage": "https://github.com/villadora/express-bunyan-logger#readme",
    "keywords": [
        "express",
        "logger",
        "bunyan"
    ],
    "license": "BSD",
    "main": "index.js",
    "maintainers": [
        {
            "name": "ecoutu",
            "email": "eric.coutu@gmail.com"
        },
        {
            "name": "marcbachmann",
            "email": "marc.brookman@gmail.com"
        },
        {
            "name": "shutterstock",
            "email": "opensource@shutterstock.com"
        },
        {
            "name": "villadora",
            "email": "jky239@gmail.com"
        }
    ],
    "name": "express-bunyan-logger",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/villadora/express-bunyan-logger.git"
    },
    "scripts": {
        "lint": "jshint index.js test/*.js",
        "test": "npm run lint && ./node_modules/.bin/mocha -R spec"
    },
    "version": "1.3.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module express-bunyan-logger](#apidoc.module.express-bunyan-logger)
1.  [function <span class="apidocSignatureSpan">express-bunyan-logger.</span>errorLogger (opts)](#apidoc.element.express-bunyan-logger.errorLogger)



# <a name="apidoc.module.express-bunyan-logger"></a>[module express-bunyan-logger](#apidoc.module.express-bunyan-logger)

#### <a name="apidoc.element.express-bunyan-logger.errorLogger"></a>[function <span class="apidocSignatureSpan">express-bunyan-logger.</span>errorLogger (opts)](#apidoc.element.express-bunyan-logger.errorLogger)
- description and source-code
```javascript
errorLogger = function (opts) {
    var logger, opts = opts || {}, format,
        immediate = false,
        parseUA = true,
        excludes,
        obfuscate,
        obfuscatePlaceholder,
        genReqId = defaultGenReqId,
        levelFn = defaultLevelFn,
        includesFn;

    if (opts.logger) {
      logger = opts.logger;
    }

    // default format
    format = opts.format || ":remote-address :incoming :method :url HTTP/:http-version :status-code :res-headers[content-length] :
referer :user-agent[family] :user-agent[major].:user-agent[minor] :user-agent[os] :response-time ms";
    delete opts.format; // don't pass it to bunyan
    (typeof format != 'function') && (format = compile(format));

    opts.hasOwnProperty('parseUA') && (parseUA = opts.parseUA, delete opts.parseUA);

    if (opts.immediate) {
        immediate = opts.immediate;
        delete opts.immediate;
    }

    if (opts.levelFn) {
        levelFn = opts.levelFn;
        delete opts.levelFn;
    }

    if (opts.excludes) {
        excludes = opts.excludes;
        delete opts.excludes;
    }

    if (opts.obfuscate) {
        obfuscate = opts.obfuscate;
        obfuscatePlaceholder = opts.obfuscatePlaceholder || '[HIDDEN]';
        delete opts.obfuscate;
        delete opts.obfuscatePlaceholder;
    }

    if (opts.includesFn) {
        includesFn = opts.includesFn;
        delete opts.includesFn;
    }


    if (opts.genReqId) {
        genReqId = typeof genReqId == 'function' ? opts.genReqId : defaultGenReqId;
    }else if (opts.hasOwnProperty('genReqId')) {
        genReqId = false;
    }

    return function (err, req, res, next) {
        var startTime = process.hrtime();

        var app = req.app || res.app;

        if (!logger) {
            opts.name = (opts.name || app.settings.shortname || app.settings.name || app.settings.title || 'express');
            opts.serializers = opts.serializers || {};
            opts.serializers.req = opts.serializers.req || bunyan.stdSerializers.req;
            opts.serializers.res = opts.serializers.res || bunyan.stdSerializers.res;
            err && (opts.serializers.err = opts.serializers.err || bunyan.stdSerializers.err);
            logger = bunyan.createLogger(opts);
        }

        var requestId;

        if (genReqId)
          requestId = genReqId(req);

        var childLogger = requestId !== undefined ? logger.child({req_id: requestId}) : logger;
        req.log = childLogger;

        function logging(incoming) {
            if (!incoming) {
                res.removeListener('finish', logging);
                res.removeListener('close', logging);
            }

            var status = res.statusCode,
                method = req.method,
                url = (req.baseUrl || '') + (req.url || '-'),
                referer = req.header('referer') || req.header('referrer') || '-',
                ua = parseUA ? useragent.parse(req.header('user-agent')) : req.header('user-agent'),
                httpVersion = req.httpVersionMajor + '.' + req.httpVersionMinor,
                hrtime = process.hrtime(startTime),
                responseTime = hrtime[0] * 1e3 + hrtime[1] / 1e6,
                ip, logFn;

            ip = ip || req.ip || req.connection.remoteAddress ||
                (req.socket && req.socket.remoteAddress) ||
                (req.socket.socket && req.socket.socket.remoteAddress) ||
                '127.0.0.1';

            var meta = {
                'remote-address': ip,
                'ip': ip,
                'method': method,
                'url': url,
                'referer': referer,
                'user-agent': ua,
                'body': req.body,
                'short-body': undefined,
                'http-version': httpVersion,
                'response-time': responseTime,
                "response-hrtime": hrtime,
                "status-code": status,
                'req-headers': req.headers,
                'res-headers': res._headers,
                'req': req,
                'res': res,
                'incoming':incoming?'-->':'<--'
            }; ...
```
- example usage
```shell
...

To use the logger:

app.use(require('express-bunyan-logger')());

To use the errorLogger:

app.use(require('express-bunyan-logger').errorLogger());

And you can also pass bunyan logger options to the logger middleware:

app.use(require('express-bunyan-logger')({
    name: 'logger',
    streams: [{
        level: 'info',
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
