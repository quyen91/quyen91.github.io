---
layout: default
title:  "[Rails] Some commands in elasticsearch"
date:   2017-09-10 15:30:46 +0700
categories: rails
tags: elasticseach
---
These are some popular basic commands used in elasticsearch
# Create index and import data
```ruby
# To delete old index, create new index and import in one command:
rake environment elasticsearch:import:model CLASS='Post' FORCE=y
# Just import and update data elasticseach
rake environment elasticsearch:import:model CLASS='Post'
```
# Create and delete index or alias
```ruby
curl -XPUT 'localhost:9200/new_index?pretty'
curl -XDELETE 'localhost:9200/exist_index?pretty'
```
# Remove many indexs same time
``` ruby
curl -XPOST localhost:9200/_aliases?pretty -d '
{
    "actions" : [
        { "remove_index": { "index": "my_index_1" } },
        { "remove_index": { "index": "my_index_2" } },
    ]
}'
```

# View all aliases and indexes
```ruby
curl -XGET 'localhost:9200/_alias?pretty'
```

# View data size of indexes
```ruby
curl -XPGET 'localhost:9200/_cat/indices?pretty'
or
curl -XGET 'localhost:9200/_cat/indices?v&pretty'

yellow open posts_v3 RHypNTRkTmGdJ3wciYvdqw 5 1 11484 0 1001.6kb 1001.6kb
yellow open users_v1 JIMJJCFxT8KHpQvLYzmaKQ 5 1   286 2   65.3kb   65.3kb
yellow open users_v2 ri6_FbGRTQGyvt5it1xA1Q 5 1     0 0     650b     650b
yellow open posts_v1 RcDU2fabRRGhydXwpQ76ag 5 1 11484 0      1mb      1mb
yellow open users    M1HXfEcERkia8PgL-N6vcQ 5 1     0 0     650b     650b
```
# View cluster size
```ruby
curl -XGET 'http://localhost:9200/_cluster/stats?human&pretty'
```
# View index size + info
```ruby
curl -XGET 'http://localhost:9200/posts/_stats&pretty'
```