Publicizr allows you to publish a post to Facebook, Twitter and Linkedin after you have published a new blog post to your Octopress blog.

###Setup

Currently you would need to create your own apps for facebook, twitter and linkedin then acquire your own user tokens.
Here are the links to the developer websites where you can create an app:

- [facebook](https://developers.facebook.com/)
- [twitter](https://apps.twitter.com/)
- [linkedin](https://www.linkedin.com/secure/developer)

After that, you would need to build an application that will allow you to retrieve user tokens. If you're primarily working on PHP you can use the following libraries to acquire user tokens:

- [thephpleagues/oauth2-client](https://github.com/thephpleague/oauth2-client) - this supports facebook and linkedin.
- [thmOAuth](https://github.com/themattharris/tmhOAuth) - supports twitter.

You also need to add the following on the Gemfile used by Octopress:

```
gem 'linkedin', '~> 1.0.0'
gem 'twitter', '~> 5.11.0'
gem 'koala', '~> 1.10.1'
gem 'em-resolv-replace', '~> 1.1.3'
```

Adding those would install the gems used for publishing to the different social networks. Once you've added those, execute `bundle install` on your terminal to install the dependencies.

Last thing that you need to do is to require the gems that we have added on the Gemfile on the Rakefile:

```
require "twitter"
require "koala"
require "linkedin"
require "resolv-replace"
```

Then add the `publish` task, be sure to comment out the corresponding code if you do not want to publish to all of the networks. Also don't forget to replace the app key, app secret, user token and user secret for each of the networks:

```
desc "Publish post to facebook, twitter and linkedin"
task :publish, :content do |t, args|
  
  if args.content
    post = args.content
    

    #post to twitter
    tweet = Twitter::REST::Client.new do |config|
      config.consumer_key        = "twitter-app-key"
      config.consumer_secret     = "twitter-app-secret"
      config.access_token        = "twitter-user-token"
      config.access_token_secret = "twitter-user-secret"
    end


    tweet.update(post)

    #post to facebook
    @graph = Koala::Facebook::API.new("facebook-user-token")
    @graph.put_wall_post(post)

    #post to linkedin
    linked_in = LinkedIn::Client.new('linkedin-app-key', 'linkedin-app-secret')
    linked_in.authorize_from_access('linkedin-user-token', 'linkedin-user-secret')

    linked_in.add_share(:comment => post)

    puts "Your post has been shared!"

  else
    puts "Supply your post!"
  end
  

end
```

###How to Use

You can use publicizr by executing the `publish` task then supplying the content of your post as an argument:

```
rake publish["new blog post: newsletters I subscribe to http://wern-ancheta.com/blog/2014/09/07/newsletters-i-subscribe-to/"]
```

###TODO

- automatically detect last post that was created
- web component that can be used to retrieve user tokens

