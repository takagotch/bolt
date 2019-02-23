### bolt
---
https://github.com/boltdb/bolt

```sh
go get github.com/boltdb/bolt/...
```

```go
package main

import (
  "log"
  
  "github.com/boltdb/bolt"
)

func main() {
  db, err := bolt.Open("my.db", 0600, nil)
  if err != nil {
    log.Fatal(err)
  }
  defer db.Close()
}


db, err := bolt.Open("my.db", 0600, &bolt.Option{Timeout: 1 * time.Second})







```

```
```


