## CODE EXAMPLES

### DECODING
- URL-Decode in Ruby: `require 'uri'; URI.decode("http%3A%2F%2Fexample.com%2F%3Fa%3Druby%20uri%20decode")`

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
