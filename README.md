### Redis
---

https://redis.io/

https://github.com/antirez/redis

https://github.com/uglide/RedisDesktopManager

http://redis.shibu.jp/
http://redis-documentasion-japanese.readthedocs.io/ja/latest/

.go
https://github.com/go-redis/redis

```c
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



























































