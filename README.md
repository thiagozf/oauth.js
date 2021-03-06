# @thiagozf/oauth-ts

[![Codecov](https://img.shields.io/codecov/c/gh/thiagozf/oauth-ts/master.svg)](https://codecov.io/gh/thiagozf/oauth-ts)
[![CircleCI](https://img.shields.io/circleci/project/github/thiagozf/oauth-ts/master.svg)](https://circleci.com/gh/thiagozf/oauth-ts)

OAuth 2.0 authentication library

## How to use

```typescript
/* MyOAuthApp.ts */
import { OpenIDProvider, OAuthApplication, resolveProvider } from 'oauth-ts';

const provider: OpenIDProvider = await resolveProvider(
  'https://my.oidc.provider.com'
);

export const oauthApp: OAuthApplication = new OAuthApplication({
  provider,
  clientId: 'my_client_id',
  redirectUri: 'http://localhost:3000/callback',
  silentRedirectUri: 'http://localhost:3000/silent-callback',
  scope: 'read write',
  flow: 'IMPLICIT'
});

/* index.ts */
import { oauthApp } from './MyOAuthApp';

if (!oauthApp.hasActiveSession()) {
  return oauthApp.login();
}

console.log(oauthApp.getUser());

/* callback.ts */
import { oauthApp } from './MyOAuthApp';

oauthApp.handleCallback();
```
