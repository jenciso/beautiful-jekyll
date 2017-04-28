---
layout: post
published: true
title: Some Tips to use in Kibana Dev Tools
bigimg: /img/kibana50console.png
---

## Search using query 

```
GET filebeat-2017.04.28/_search
{
  "query": {
    "match": {
      "type": {
        "query": "smtp-relay-log",
        "type": "phrase"
      }
    }
  }
}

## Delete using query

```
POST filebeat-2017.04.28/_delete_by_query
{
  "query": {
    "match": {
      "type": {
        "query": "smtp-relay-log",
        "type": "phrase"
      }
    }
  }
}
```


