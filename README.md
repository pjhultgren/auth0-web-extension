# auth0-web-extension

## Installation

Using [npm](https://npmjs.org)

```sh
npm install https://github.com/pjhul/auth0-web-extension
```

Using [yarn](https://yarnpkg.com)

```sh
yarn add auth0-web-extension@https://github.com/pjhul/auth0-web-extension
```

## Create the token handler

Add the following code to your service worker:

```js
import { handleTokenRequest } from "auth0-web-extension"

handleTokenRequest(<YOUR_REDIRECT_URI>);
```

## Permissions

In your manifest, you will need to add a couple items.

```jsonc
{
  /* ... */
  "content_scripts": [
    {
      "matches": [
        "...",
        "<YOUR_REDIRECT_URI>" // Make sure your redirect url is included
      ],
      "all_frames": true, // All frames must be set to true
      "js": ["..."]
    }
  ]
}
```

## Initializing the client

In your background script, create an `Auth0Client` instance

```js
import createAuth0Client from "auth0-web-extension"

const auth0 = createAuth0Client({
  domain: '<AUTH0_DOMAIN>',
  client_id: '<AUTH0_CLIENT_ID>',
  redirect_uri: '<YOUR_REDIRECT_URI>',
});
```

## Get an access token

Now, all you need to do to get an access token, is to call `getTokenSilently`

```js
const token = await auth0.getTokenSilently(options);
```

## Caveats

1. You will **only** be able to retrieve access tokens in your background script if there is at least one instance of your service worker running.
2. We don't yet support refresh tokens, but again this should be coming soon.
3. This package is not on npm yet, but after some of these other caveats are fixed I'll make it available.

## Support + Feedback

For support or to provide feedback, please [raise an issue on the issue tracker](https://github.com/pjhul/auth0-web-extension/issues).

## License

This project is licensed under the MIT license. See the [LICENSE](https://github.com/pjhul/auth0-web-extension/blob/main/LICENSE) file for more info.
