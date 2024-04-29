# Overview

Creates a express server using NodeJS which exposes below endpoints to complete OAuth using PKCE Flow

# @affinidi/passport-affinidi

@affinidi/passport-affinidi is a powerful module for authenticating users with `Affinidi Login` using the OIDC Code Grant flow. This strategy seamlessly integrates `Affinidi Login` into your Node.js applications. By leveraging Passport, you can effortlessly incorporate Affinidi authentication into any application or framework that supports Connect-style middleware, including Express.

This provider simplifies the process by creating an Affinidi OpenID client and registering two essential routes:

1. **Initialization Route**: The first GET route (defaulted to `/api/affinidi-auth/init`) returns the Affinidi authorization URL, which allows frontend applications to redirect to Affinidi Login flow.
2. **Completion Route**: The second POST route (defaulted to `/api/affinidi-auth/complete`) processes the response (code and state) from Affinidi authorization server, performs the exchange for the ID Token, and returns the user's profile.

## Installation

```
npm install @affinidi/passport-affinidi
```

## Usage
Here's how to use `@affinidi/passport-affinidi` in your Node.js application:

1. Import the affinidi provider

```
import { affinidiProvider } from '@affinidi/passport-affinidi'
```

2. Initialize the provider by passing your express server instance and configuration options, including the Affinidi's issuer, client ID, secret, and redirect URIs.

```
 await affinidiProvider(app, {
        id: "affinidi",
        issuer: process.env.AFFINIDI_ISSUER,
        client_id: process.env.AFFINIDI_CLIENT_ID,
        pkce: true,
        redirect_uris: ['http://localhost:3000/auth/callback']
    });
```
3. Create Affinidi Login configuration with Authentication Mode as 'None', you can find same PEX & ID Token mapping [here](/profile-pex.json)


## Run the App

```
node index.js
```


## Sample API Calls using CURL
Here's how to initiate and complete the Affinidi from your frontend:

1. Initiate the Affinidi flow

```
curl --location 'http://localhost:3001/api/affinidi-auth/init'
```

2. Complete the Affinidi flow from callback url and get user profile/error

```
curl --location 'http://localhost:3001/api/affinidi-auth/complete' \
--header 'Content-Type: application/json' \
--data '{
    "code": "ory_ac_snkiJvamz56ZhE4vRvS_zjfHDwKzDQ7ADsQecQ9EQJ8.WXNLV47p7yZnbvp0_SwvFErO3JpvIEQme_X7ACW8WGA",
    "state": "crM6FIM6VU8g0BDHI332GfM1iQe5A5Z1EqHmdGUsQqw"
}'
```
