## Reading materials
* [Github - Building a CI serve](https://developer.github.com/guides/building-a-ci-server/)
* [Github - Webhooks](https://developer.github.com/enterprise/2.7/webhooks/)
* [Github API - Statuses](https://developer.github.com/v3/repos/statuses/)

## Steps
* Create a webhook by following the above links
* [Setup ngrok](https://ngrok.com/docs#getting-started) for setting up secue tunnel to the server
```
$ ngrok http 3000
```
* Create a service that can receive the Github events and calls to the CI server.

Here is some example code I used to create a NodeJS service using KOA.

```Javascript
const Koa = require('koa');
const Router = require('koa-router');
const KoaBody   = require('koa-body');
const GitHubApi = require("github");

const app = new Koa();
const router = new Router();
const koaBody = KoaBody();
const owner = 'xzdev';
const repo = 'github-ci';

const github = new GitHubApi({
    // optional
    debug: true,
    protocol: "https",
    host: "api.github.com", // should be api.github.com for GitHub
    pathPrefix: "/api/v3", // for some GHEs; none for GitHub
    headers: {
        "user-agent": "Node-GitHub-App" // GitHub is happy with a unique user agent
    },
    Promise: require('bluebird'),
    followRedirects: false, // default: true; there's currently an issue with non-get redirects, so allow ability to disable follow-redirects
    timeout: 5000
});

github.authenticate({
    type: "basic",
    username: 'xzdev',
    password: '****'
});

router.post('/event_handler', koaBody, (ctx, next) => {
    const pullRequest = ctx.request.body.pull_request;
    const {statuses_url, number} = pullRequest;
    console.log('event requst', pullRequest);
    // call ci api to start End2End test
    // $ git fetch origin pull/{number}/head:{branchName}
    // $ git checkout {branchName}
}).post('/cicallback_handler', koaBody, (ctx, next) => {
    const { sha, targetUrl, state, description }  = ctx.request.body;
    github.repos.createStatus({
        owner,
        repo,
        sha,
        state,
        description,
        context: 'CI agent',
        target_url: targetUrl
    });
});


app.use(router.routes())
    .use(router.allowedMethods());

```

The content of the package.json.

```
{
  "name": "github-ci",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "bluebird": "^3.4.7",
    "github": "^8.1.1",      
    "koa": "^2.0.0",
    "koa-body": "^2.0.0",
    "koa-router": "^7.0.1"
  }
}
```