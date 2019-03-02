### Redis
---

https://redis.io/

.c
https://github.com/antirez/redis

https://github.com/uglide/RedisDesktopManager

.ruby
http://redis.shibu.jp/
http://redis-documentasion-japanese.readthedocs.io/ja/latest/

.go
https://github.com/go-redis/redis


```
make
%make 32bit
make test
make distclean
make MALLOC=libc
make MALLOC=jemalloc
make V=1
cd src
./redis-server

cd src
./redis-server /path/to/redis.conf

./redis-server --port 9999 --replicaof 127.0.0.1 6379
./redis-server /etc/redis/6379.conf --loglevel debug

cd src
./redis-cli

make install
cd utils
./install_server.sh
```

```c
struct client {
  int fd;
  sds querybufl
  int argc;
  robj **argv;
  redisDb *db;
  int flags;
  list *reply;
  char buf[PROTO_REPLY_CHUNK_BYTES];
}

typedef struct redisObject {
  unsigned type:4;
  unsigned encoding:4;
  unsighed lru:LRU_BITS;
  int refcount;
  void *ptr;
} robj;

void foobarCommand(client *c) {
  printf("%s", c->argv[1]->ptr);
  addReply(c,shard.ok);
}
```

```
{"foobar",foobarCommand,2,"rfF",0,NULL,0,0,0,0,0},
```

```ruby
require 'rubygems'
require 'redis'

def bench(descr)
  start = Time.now
  yield
  puts "#{descr} #{Time.now-start} seconds"
end

def with_pipelining
  r = Redis.new
  r.pipelined {
    10000.times {
      r.ping
    }
  }
end

bench("without pipelining") {
  without_pipelining
}
bench("with pipelining") {
  with_pipelining
}


```

```go
import "github.com/go-redis/redis"


func ExampleNewClient() {
  client := redis.NewClient(&redis.Options{
    Addr: "localhost:6379",
    Password: "",
    DB: 0,
  })
  
  pong, err := client.Ping().Result()
  fmt.Println(pong, err)
}

func ExampleClient() {
  err := client.Set("key", "value", 0).Err()
  if err != nil {
    panic(err)
  }
  
  val, err := client.Get("key").Result()
  if err != nil{
    panic(err)
  }
  fmt.Println("key", val)
  
  val2, err := client.Get("key2").Result()
  if err == redis.Nil {
    fmt.Println("key2 does not exist")
  } else if err != nil {
    panic(err)
  } else {
    fmt.Println("key2", val2)
  }
}


set, err := client.SetNX("key", "value", 10*time.Second).Result()

vals, err := client.Sort("list", redis.Sort{Offset: 0, Count: 2, Order: "ASC"}).Result()

vals, err := client.ZRangeByScoreWithScores("zset", redis.ZRangeBy{
  Min: "-inf",
  Max: "+inf",
  Offset: 0,
  Count: 2,
}).Result()

vals, err := client.ZInterStore("out", redis.ZStore(Weights: []int64{2, 3}), "zset1", "zset2").Result()

vals, err := client.Eval("return {KEYS[1],ARGV[1]}", []string{"key"}, "hello").Result()
```



























































