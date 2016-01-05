Publicizr allows you to publish a post to Facebook, Twitter and Linkedin after you have published a new blog post to your Octopress blog.

###Dependencies

You can find the dependencies of this project in the `Gemfile`. Just add those to the `Gemfile` of your octopress installation and execute `bundle install` to install all of them.

###Setup

You can setup publicizr in two ways: first is by setting up the [ahead project](http://github.com/anchetaWern/ahead) on your machine. Once you have created an account and connected your social accounts. Go to the settings page and copy your API key and add it as a value for the `api_key`. Be sure to set the value for `use_ahead` as `true` if you want to use your ahead account for publishing:

```
[user]
use_ahead=true
api_key=YOUR_AHEAD_API_KEY
ahead_base_url=http://ahead.dev
```

One thing to remember when using ahead with publicizr is that it uses the default social accounts that you have selected on your settings page. So be sure to select a default account if you haven't done so.

The second option is by acquiring an oauth token for each social accounts you want to connect, get the API credentials for those and add them to the `user.ini` file:

```
[user]
use_ahead=false
ahead_base_url=http://ahead.dev
api_key=YOUR_AHEAD_API_KEY
twitter_api=YOUR_TWITTER_API_KEY
twitter_secret=YOUR_TWITTER_SECRET_KEY
twitter_usertoken=YOUR_TWITTER_USER_TOKEN
twitter_usersecret=YOUR_TWITTER_USER_SECRET
fb_usertoken=YOUR_FACEBOOK_USER_TOKEN
linkedin_appkey=YOUR_LINKEDIN_APP_KEY
linkedin_appsecret=YOUR_LINKEDIN_APP_SECRET
linkedin_usertoken=YOUR_LINKEDIN_USER_TOKEN
linkedin_usersecret=YOUR_LINKEDIN_USER_SECRET
```

Here are the links for the developer websites:

- [facebook](https://developers.facebook.com/)
- [twitter](https://apps.twitter.com/)
- [linkedin](https://www.linkedin.com/secure/developer)

You can acquire oauth tokens by creating an app in the websites that I mentioned above. If you're primarily working on PHP you can use the following libraries to acquire user tokens:

- [thephpleagues/oauth2-client](https://github.com/thephpleague/oauth2-client) - this supports facebook and linkedin.
- [thmOAuth](https://github.com/themattharris/tmhOAuth) - supports twitter.

Next, copy the contents of the `Rakefile` in this repository and add them to the `Rakefile` of your octopress installation.

Note that both methods require you to create an app which will serve as the connection to your social account.

###How to Use

You can use publicizr by executing the `publish` task then supplying the content of your post as an argument:

```
rake publish["new blog post: newsletters I subscribe to http://wern-ancheta.com/blog/2014/09/07/newsletters-i-subscribe-to/"]
```

###TODO

- support for buffer app
- automatically detect last post that was created


##License

The MIT License (MIT) Copyright (c)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.