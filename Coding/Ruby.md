## CODE EXAMPLES

### PROXY
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
