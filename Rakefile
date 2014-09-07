require "twitter"
require "koala"
require "linkedin"
require "resolv-replace"

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
