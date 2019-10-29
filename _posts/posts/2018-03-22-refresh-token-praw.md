---
layout: post
title: Use refresh tokens with PRAW
date: 2018-03-22 01:00:00
link: /posts/refresh-token-praw
categories: posts
description: Authenticating your Reddit bot via a refresh token with PRAW
keywords: "Reddit, bot, API wrapper, username, password, OAuth, PRAW"
parentPost: true
authors:
    - PeskyPotato
---

## Introduction
This is intended for users who already have a basic understanding of [PRAW](https://praw.readthedocs.io/en/latest/) and want to switch from hard coding the username and password into their code to using a refresh token. This was written using PRAW version 6.1.1 and Python 3.7.1. To let you in on a secret, I initially wrote for myself so I don't forget how I did it.

## Create an app
Create an application [through preferences](https://www.reddit.com/prefs/apps/) with a title and description, the about URL can be left blank. Choose "script" for the type and enter the redirect URI `https://127.0.0.1:65010/authorize_callback`.

If this is your first time creating a bot, make sure you have read the [API usage guidelines.](https://www.reddit.com/wiki/api).

## Get the authentication URL
In a new python file add the client id and secret along with the user agent and set the redirect URL to `https://127.0.0.1:65010/authorize_callback`. Next make a request for the authentication URL, with all the [releveant scopes.](https://www.reddit.com/dev/api/oauth) The duration here is set to permanent so that we do not need to reauthenticate.

```
import praw
from uuid import uuid4

reddit = praw.Reddit(client_id='',
                    client_secret='',
                    user_agent='',
                    redirect_uri='https://127.0.0.1:65010/authorize_callback')

state_end = str(uuid4())
authlink = reddit.auth.url(['submit'], state_end, duration='permanent')
print(state_end)
print(authlink)
```

The authentication url will be printed.

## Login
Open the authentication URL in a browser and login in using the account you wish to use for the bot. This does not need to be the same account you used to create the API credentials.

After signing in, give permission.

## Refresh token
Now you will be redirected to a page that is not available, do not fret! Copy the code parameter from the URL ( the bit after `&code=`).

Using this code, we need to authorize in order to get our refresh token. 

```
print(reddit.auth.authorize('ENTER CODE HERE'))
```

What is printed out is our refresh token. 

## Update Reddit instance
Finally, we can put this fresh token to use. 

```
reddit = praw.Reddit(client_id='',
                    client_secret='',
                    user_agent='',
                    refresh_token='',
                    redirect_uri='https://127.0.0.1:70000')
```
Since we only gave submit permissions, I am going to print out the scope and then submit a post to /r/test.

```
print(reddit.auth.scopes())
reddit.subreddit('test').submit(str("testing, 123"), url='http://google.com')
```

## Further reading

[How to make your bot use OAuth2](https://www.reddit.com/r/GoldTesting/comments/3cm1p8/how_to_make_your_bot_use_oauth2/) - A now depreciated guide on authentication

[PRAW docs](https://praw.readthedocs.io/en/latest/getting_started/authentication.html#read-only-mode) - Official PRAW documentation on authentication 

[Reddit API doc](https://www.reddit.com/dev/api/oauth/) - Official Reddit API documentation on OAuth


All done!

`:)`
