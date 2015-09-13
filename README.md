## Cloud Code in Express/Node.JS

Take your existing cloud code files and place them in the `cloud/` folder.  Add the following line at the very top of each file:

```
var Parse = require('parse-cloud-express').Parse;
```

Set up some environment variables:

```
export PARSE_APP_ID=yourappid
export PARSE_MASTER_KEY=yourmasterkey
export PARSE_WEBHOOK_KEY=yourkeyhere
```

Download all required dependencies with:

```
npm install
```

Run your new server:

```
node server.js
```

### Local testing

Set up [ngrok](https://ngrok.io) and once your server is launched, run ngrok in a different terminal window:

```
// Port 5000 is provided as a default in server.js, can be changed by PORT environment variable
ngrok http 5000
```

Take the URL provided by ngrok, set it as an environment variable, and run the script to register your webhooks with Parse:

```
export HOOKS_URL=https://something.ngrok.io
npm run register
```


### Caveats

Cloud Code required you to use `cloud/` as a prefix for all other .js files, even though they were in the same folder.  That doesn't apply here, so you'll need to update any require statements in files under `cloud/` to reference just `./` instead.

The first-party modules hosted by Parse will not be available (sendgrid, mailgun, stripe, image, etc.) and you'll need to update your code to use the official modules available via npm.

The base mount path is set in both `server.js` and `scripts/register-webhooks.js` and must be equal.

