require 'twitter'
require 'koala'
require 'linkedin'
require 'resolv-replace'
require 'net/http'
require 'inifile'

desc "Publish post to facebook, twitter and linkedin"
task :publish, :content do |t, args|

  if args.content
    post = args.content

    file = IniFile.load('user.ini')
    config = file['user']

    if config['use_ahead'] == true

      uri = URI.parse(config['ahead_base_url'])
      http = Net::HTTP.new(uri.host, uri.port)
      http.use_ssl = false
      http.verify_mode = OpenSSL::SSL::VERIFY_NONE
      request = Net::HTTP::Post.new("/api/post")
      request.set_form_data({'api_key' => config['api_key'], 'content' => post})

      response = http.request(request)
      puts response.body

    else
      #post to twitter
      tweet = Twitter::REST::Client.new do |c|
        c.consumer_key        = config['twitter_api']
        c.consumer_secret     = config['twitter_secret']
        c.access_token        = config['twitter_usertoken']
        c.access_token_secret = config['twitter_usersecret']
      end


      tweet.update(post)

      #post to facebook
      @graph = Koala::Facebook::API.new(config['fb_usertoken'])
      @graph.put_wall_post(post)

      #post to linkedin
      linked_in = LinkedIn::Client.new(config['linkedin_appkey'], config['linkedin_appsecret'])
      linked_in.authorize_from_access(config['linkedin_usertoken'], config['linkedin_usersecret'])

      linked_in.add_share(:comment => post)

      puts "Your post has been shared!"
    end

  else
    puts "Supply your post!"
  end


end
