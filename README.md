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

```



























































