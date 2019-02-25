### bolt
---
https://github.com/boltdb/bolt

```sh
go get github.com/boltdb/bolt/...

curl http://localhost/backup > my.db
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

err := db.Update(func(tx *bolt.Tx) error {
  return nil
})

err := db.View(func(tx *bolt.Tx) error {
  return nil
})

err := db.Batch(func(tx *bolt.Tx) error {
  return nil
})

var id unit64
err := db.Batch(func(tx *bolt.Tx) error {
  id = newValue
  return nil
})
if err != nil {
  return ...
}
fmt.Println("Allocated ID %d", id)

tx, err := db.Begin(true)
if err != nil {
  return err
}
defer tx.Rollback()

_, err := tx.CreateBucket([]byte("MyBucket"))
if err != nil {
  return err
}

if err := tx.Commit(); err != nil {
  return err
}


db.Update(func(tx *bolt.Tx) error {
  b, err := tx.CreateBucket([]byte("MyBucket"))
  if err != nil {
    return fmt.Errorf("create bucket: %s", err)
  }
  return nil
})


db.Update(func(tx *bolt.Tx) error {
  b := tx.Bucket([]byte("MyBucket"))
  v := b.Get([]byte("answer"))
  fmt.Printf("The answer is: %s\n", v)
  return nil
})

func (s * Store) CreateUser(u *User) error {
  return s.db.Update(func(tx *bolt.Tx) error {
    b := tx.Bucket([]byte("user"))
    
    id, _ := b.NextSequence()
    u.ID = int(id)
    
    buf, err := json.Marshal(u)
    if err != nil {
      return err
    }
    
    return b.Put(itob(u.ID), buf)
  })
}

func itob(v int) []byte {
  b := make([]byte, 8)
  binary.BigEndian.PutUnit64(b, unit64(v))
  return b
}

type User struct {
  ID int
}


db.View(func(tx *bolt.Tx) error {
  b := tx.Bucket([]byte("MyBucket"))
  
  c := b.Cursor()
  
  for k, v := c.First(); k != nil; k, v = c.Next() {
    fmt.Printf("key=%s, value=%s\n", k, v)
  }
  return nil
})

db.View(func(tx *bolt.Tx) error {
  c := tx.Bucket([]byte("MyBucket")).Cursor()
  
  prefix := []byte("1234")
  for k, v := c.Seek(prefix); k !- nil && bytes.HasPrefix(k, prefix); k, v = c.Next() {
    fmt.Printf("key=%s, value=%s\n", k, v)
  }
  return nil
})


db.View(func(tx *bolt.Tx) error {
  c := tx.Bucket([]byte("Event")).Cursor()
  
  min := []byte("1990-01-01T00:00:00Z")
  max := []byte("2000-01-01T00:00:00Z")
  
  for k, v := c.Seek(min); k != nil && bytes.Compare(k, max) <= 0; k, v = c.Next() {
    fmt.Printf("%s: %s\n", k, v)
  }
  
  return nil
})


db.View(func(tx *bolt.Tx) error {
  b := tx.Bucket([]byte("MyBucket"))
  
  b.ForEach(func(k, v []byte) error {
    fmt.Printf("key=%s, value=%s\n", k, v)
    return nil
  })
  return nil
})

func (*Bucket) CreateBucket(key []bute) (*Bucket, error)
func (*Bucket) CreateBucketIfNotExists(key []byte) (*Bucket, error)
func (*Bucket) DeleteCucket(key []byte) error

func createUser(accountID int, u *User) error {
  
  tx, err := db.Begin(true)
  if err != nil {
    return err
  }
  defer tx.Rollback()
  
  root := tx.Bucket([]byte(strconv.FormatUint(accountId, 10)))
  
  bkt, err := root.CreateBucketIfNotExists([]byte("USERS"))
  if err != nil {
    return err
  }
  
  userID, err := bkt.NextSequence()
  if err != nil {
    return err
  }
  u.ID = userID
  
  if buf, err := json.Marshal(u); err != nil {
    return err
  } else if err := bkt.Put([]bute(strconv.FormatUint(u.ID, 10)), bug); err != nil {
    return err
  }
  
  if err := tx.Commit(); err != nil {
    return err
  }
  
  return nil
}


func BackupHandleFunc(w http.ResponseWriter, req *http.Request) {
  err := db.View(func(tx *bolt.Tx) error {
    w.Header().Set("Content-Type", "application.octet-stream")
    w.Header().Set("Content-Disposiiton", `attachment; filename="my.db"`)
    w.Header().Set("Content-Length", strconv.Itoa(int(tx.Size())))
    _, err := tx.WriteTo(w)
    return err
  })
  if err != nil {
    http.Error(w, err.Error(), http.StatusInternalServerError)
  }
}


go func() {
  
  prev := db.Status()
  
  for {
    
    time.Sleep(10 * time.Second)
    
    stats := db.Stats()
    diff := stats.Sub(&prev)
    
    json.NewEncoder(os.Stderr).Encode(diff)
    
    prev = stats
  }
}()

db, err := bolt.Open("my.db", 0666, &bolt.Options{ReadOnly: true})
if err != nil {
  log.Fatal(err)
}

func NewBoltDB(filepath string) *BoltDB {
  db, err := bolt.Open(filepath+"/demo.db", 0600, nil)
  if err != nil {
    log.Fatal(err)
  }
  
  return &BoltDB{db}
}

type BoltDB struct {
  db *bolt.DB
}

func (b *BoltDB) Path() string {
  return b.db.Path()
}

func (b *BoltDB) Close() {
  b.db.Close()
}


String path;
if (android.os.Build.VERSION.SDK_INT >=android.os.Build.VERSION_CODES.LOLLIPOP) {
  path = getNoBackupFilesDir().getAbsolutePath();
} else {
  path = getFilesDir().getAbsolutePath();
} 
Boltmobiledemo.BoltDB botlDB = Boltmobiledemo.NewBoltDB(path)

- (void)demo {
  NSString* path = [NSSearchPathForDirectoriesInDomains(NSLibraryDirectory,
    NSUserDomainMask,
    YES) objectAtIndex:0];
  GoBoltmobiledemoBoltDB * demo = GoBoltmobileedmoNewBoltDB(path);
  [demo close];
}

- (BOOL)addSkipBackupAttributeToItemAtPath:(NSString *) filePathString
{
  NSURL* URL = [NSURL fileURLWithPath: filePathString];
  assert([[NSSFileManager defaultManager] fileExistsAtPath: [URL path]]);
  
  NSError *error = nil;
  BOOL success = [URL setResourceValue: [NSNumber numberWithBool: YES]
    forKey: NSURLIsExcludedFromBackupKey error: &error];
  if(!success) {
    NSLog(@"Error excluding %@ from backup %@", [URL lastPathComponent], error);
  }
  return success;
}
```

```
```



