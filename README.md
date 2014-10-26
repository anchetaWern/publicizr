Publicizr allows you to publish a post to Facebook, Twitter and Linkedin after you have published a new blog post to your Octopress blog.

###Dependencies

You can find the dependencies of this project in the `Gemfile`. Just add those to the `Gemfile` of your octopress installation and execute `bundle install` to install all of them.

###Setup

You can setup publicizr in two ways: first is by creating an [ahead account](http://ec2-54-68-251-216.us-west-2.compute.amazonaws.com/). Once you have created an account and connected your social accounts. Go to the settings page and copy your API key and add it as a value for the `api_key`. Be sure to set the value for `use_ahead` as `true` if you want to use your ahead account for publishing:

```
[user]
use_ahead=true
api_key=YOUR_AHEAD_API_KEY
```

The second option is by creating an app for whichever social accounts you want to connect, get the api credentials for those and add them to the `user.ini` file:

```
[user]
use_ahead=false
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

After that, you would need to build an application that will allow you to retrieve user tokens. If you're primarily working on PHP you can use the following libraries to acquire user tokens:

- [thephpleagues/oauth2-client](https://github.com/thephpleague/oauth2-client) - this supports facebook and linkedin.
- [thmOAuth](https://github.com/themattharris/tmhOAuth) - supports twitter.

Next, copy the contents of the `Rakefile` in this repository and add them to the `Rakefile` of your octopress installation.


###How to Use

You can use publicizr by executing the `publish` task then supplying the content of your post as an argument:

```
rake publish["new blog post: newsletters I subscribe to http://wern-ancheta.com/blog/2014/09/07/newsletters-i-subscribe-to/"]
```

###TODO

- support for buffer app
- automatically detect last post that was created

