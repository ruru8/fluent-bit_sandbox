# fluent-bit_sandbox

## 準備

```zsh
$ docker build -t self-fluent-bit .
```

## 実行

```zsh
$ docker run self-fluent-bit:latest /fluent-bit/bin/fluent-bit -c fluent-bit.conf

Fluent Bit v1.5.2
* Copyright (C) 2019-2020 The Fluent Bit Authors
* Copyright (C) 2015-2018 Treasure Data
* Fluent Bit is a CNCF sub-project under the umbrella of Fluentd
* https://fluentbit.io

[2020/08/20 09:04:05] [ info] [engine] started (pid=1)
[2020/08/20 09:04:05] [ info] [storage] version=1.0.4, initializing...
[2020/08/20 09:04:05] [ info] [storage] in-memory
[2020/08/20 09:04:05] [ info] [storage] normal synchronization mode, checksum disabled, max_chunks_up=128
[2020/08/20 09:04:05] [ info] [sp] stream processor started
[0] input: [1597914245.990787000, {"message"=>{"service"=>"First"}}]
[1] input: [1597914245.990811900, {"message"=>{"service"=>"Second"}}]
[0] second: [1597914245.990811900, {"message"=>{"service"=>"Second"}}]
[0] first: [1597914245.990787000, {"message"=>{"service"=>"First"}}]
[0] input: [1597914246.990942800, {"message"=>{"service"=>"First"}}]
[1] input: [1597914246.990957600, {"message"=>{"service"=>"Second"}}]
[0] second: [1597914246.990957600, {"message"=>{"service"=>"Second"}}]
....
```

## その他

### Tag が first だけ出力する

- conf の OUTPUT を書き換える

```fluent-bit.conf
[OUTPUT]
    Name   stdout
    Match  first
```

- build して実行

```zsh
$ docker build -t self-fluent-bit .
$ docker run self-fluent-bit:latest /fluent-bit/bin/fluent-bit -c fluent-bit.conf

Fluent Bit v1.5.2
* Copyright (C) 2019-2020 The Fluent Bit Authors
* Copyright (C) 2015-2018 Treasure Data
* Fluent Bit is a CNCF sub-project under the umbrella of Fluentd
* https://fluentbit.io

[2020/08/20 09:21:51] [ info] [engine] started (pid=1)
[2020/08/20 09:21:51] [ info] [storage] version=1.0.4, initializing...
[2020/08/20 09:21:51] [ info] [storage] in-memory
[2020/08/20 09:21:51] [ info] [storage] normal synchronization mode, checksum disabled, max_chunks_up=128
[2020/08/20 09:21:51] [ info] [sp] stream processor started
[0] first: [1597915311.785262300, {"message"=>{"service"=>"First"}}]
[0] first: [1597915312.785472200, {"message"=>{"service"=>"First"}}]
[0] first: [1597915313.752818700, {"message"=>{"service"=>"First"}}]
[0] first: [1597915314.752761000, {"message"=>{"service"=>"First"}}]
...

```
