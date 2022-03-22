## CODE EXAMPLES

### DECODING
- URL-Decode in Ruby: `require 'uri'; URI.decode("http%3A%2F%2Fexample.com%2F%3Fa%3Druby%20uri%20decode")`

<br />

### OAUTH2 TOKEN 
- Firstly, `gem install oauth2`
```
require 'oauth2'

callback = "http://yourMaliciousServer.com"
app_id = " "

secret = " "
client = OAuth2::Client.new(app_id, secret, site: "http://authorization-server.com")
client.auth_code.authorize_url(redirect_uri: callback)


code = " "
access = client.auth_code.get_token( code, redirect_uri: callback)
access.get("/api/user").parsed

puts access.token
```

<br />

### PROXY
- More Advanced: [https://gist.github.com/jhnbwrs/dff50c0c9515f2358ac0](https://gist.github.com/jhnbwrs/dff50c0c9515f2358ac0)
```
# REQ: sudo gem install sinatra

require 'net/http'
require 'uri'
require 'sinatra'

set :port, 4444
set :bind, '0.0.0.0'

get '/' do
  uri = URI("http://...")
  resp = Net::HTTP.get_response(uri)
  loc = resp.header['location']
  text = "Hello Visitor!"
end
```
