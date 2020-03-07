---
layout: default
title:  "Change elasticsearch mappings in rails!"
date:   2017-09-12 15:30:46 +0700
categories: rails
tags: elasticsearch
---

To change mappings and reindex elasticsearch data with zero downtime:
+ Create an alias that using to search for model (this point to whatever index we want)
+ Point this alias to old index (avoid app crash when code change)
+ Create new index + import data to this index
+ Point our alias to new index
+ Delete old index

```ruby
# Add alias user_docs to users index
curl -XPUT 'localhost:9200/users/_alias/user_docs?pretty'
curl -XGET 'localhost:9200/user_docs/_search' # Test if working

# create new users_v1 index
curl -XPUT 'localhost:9200/users_v1'

# Import
 User.import index: 'users_v1', type: 'user', force:true
 rake environment elasticsearch:import:model CLASS='User' INDEX='users_v1' FORCE=y

# Add alias to users_v1 index
curl -XPUT 'localhost:9200/users_v1/_alias/user_docs?pretty'

# one command
curl -XPOST localhost:9200/_aliases -d '
        {
            "actions": [
                { "remove": {
                    "alias": "user_docs",
                    "index": "users"
                }},
                { "add": {
                    "alias": "user_docs",
                    "index": "users_v1"
                }}
            ]
        }'

# Delete old data index
curl -XDELETE 'localhost:9200/users'

# Callback reindex when data change
 User.last.__elasticsearch__.index_document refresh: true, index: 'users_v1'

# Change index search in search query
class User
  def self.search_user()
    # ....
    return __elasticsearch__.search(search_definition, {index: 'user_docs'})
  end
end

```

Reference:
- [rails model elasticsearch import](https://github.com/elastic/elasticsearch-rails/blob/master/elasticsearch-model/lib/elasticsearch/model/importing.rb#L65)
- [rails search elasticsearch definition](https://github.com/elastic/elasticsearch-rails/blob/master/elasticsearch-model/lib/elasticsearch/model/searching.rb)
- [change aliases elasticsearch](https://stackoverflow.com/questions/29508955/elasticsearch-reindexing-your-data-with-zero-downtime)
- [change mapping with zero downtime](https://www.elastic.co/guide/en/elasticsearch/guide/current/index-aliases.html)