# Members Ssr

## Install

`npm install members-ssr --save`

or

`yarn add members-ssr`


## Usage

```js
const MembersSSR = require('./');

const {
    exchangeTokenForSession,
    getMemberDataFromSession
} = MembersSSR({
    cookieMaxAge: 1000 * 60 * 60 * 24 * 184, // 184 days max cookie age (default)
    cookieSecure: true, // Secure cookie (default)
    cookieName: 'members-ssr', // Name of cookie (default)
    cookiePath: '/', // Path of cookie (default)
    cookieKeys: 'some-coole-secret', // Key to sign cookie with
    membersApi: membersApiInstance // Used to fetch data and verify tokens
});

require('http').createServer((req, res) => {
    if (req.method.toLowerCase() === 'post') {
        exchangeTokenForSession(req, res).then(() => {
            res.writeHead(200);
            res.end();
        }).catch((err) => {
            res.writeHead(err.code);
            res.end(err.message);
        });
    } else {
        getMemberDataFromSession(req, res).then((member) => {
            res.writeHead(200, {
                'Content-Type': 'application/json'
            });
            res.end(JSON.stringify(member));
        }).catch((err) => {
            res.writeHead(err.code);
            res.end(err.message);
        });
    }
}).listen(3665);
```


## Develop

This is a mono repository, managed with [lerna](https://lernajs.io/).

Follow the instructions for the top-level repo.
1. `git clone` this repo & `cd` into it as usual
2. Run `yarn` to install top-level dependencies.


## Run

- `yarn dev`


## Test

- `yarn lint` run just eslint
- `yarn test` run lint and tests




# Copyright & License

Copyright (c) 2019 Ghost Foundation - Released under the [MIT license](LICENSE).