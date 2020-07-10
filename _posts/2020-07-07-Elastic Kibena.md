---
layout: post
title: "Elastic"
description: 
headline: 
modified: 2020-07-07
category: webdevelopment
imagefeature: cover3.jpg
tags: [Elastic Kibena]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Elastic

https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.0-windows-x86_64.zip
elasticsearch.yml 
network.host : localhost
http.port : 9200




# Kibena

https://artifacts.elastic.co/downloads/kibana/kibana-7.8.0-windows-x86_64.zip
kibana.yml
server.port:5601 - 키바나의 연결 할 포트번호를 입력해줍니다.
server.host:"localhost" - 키바나의 연결 할 주소를 입력해줍니다.
elasticsearch.hosts:["http://localhost:9200"] - 엘라스틱 서치의 주소를 입력해줍니다.


# docker

docker run --name elastic7.0 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.0.0


docker run -d --rm --link elastic7.0:elastic-url -e "ELASTICSEARCH_HOSTS=http://elastic-url:9200" -p 5601:5601 --name kibana7.0 docker.elastic.co/kibana/kibana:7.0.0


## index
Kibena -> dev -> tool

```JavaScript
PUT /imo
{
    "settings":{
        "number_of_shards":1,
        "number_of_replicas":1
    },
    "mappings":{
        "properties":{
            "name":{
                "type":"text"
            },
            "id":{
                "type":"integer"
            },
            "imo":{
                "type":"text"
            }
        }
    }

}


GET /movie/_mapping

POST /movie/_doc
{
    "name":"your vsl name",
    "id":1,
    "imo":"12345"
}


GET /movie/_search
{
    "query":{
        "match":{
            "name":"your vsl name"
        }
    }
}

DELETE /movie
{
    "query":{
        "match":{
            "name":"vsl name"
        }
    }
}

```

## Elasticsearch의 Relevance 계산 알고리즘(TF-IDF)

The standard similarity algorithm used in Elasticsearch

- TF(Term Frequency)

문서 내 발생한 term 빈도수가 클수록 weight가 높다. 문서내에서 같은 단어가 여러번 등장한다면 그 단어에 높은 가중치를 주는 알고리즘이다.

- IDF(Inverse Document Frequency)

전체 문서에서 발생한 term 빈도수가 작을수록 weight가 높다. 문서에 자주 등장하는 단어일수록 낮은 가중치를 주는 알고리즘이다.

똑같이 1번 검색이 되었다 하더라도 문서에 자주 등장한 단어가 매칭된 키워드일수록 낮은 가중치를 가지게 된다.

문서에 많이 나오는게 좋은게 아닌가? 라고 생각할 수 있겠지만 문서에 공통적으로 많이 등장하는 단어는 실제 우리가 쓰는 단어로 살펴본다면 "은", "는", "다"처럼 형용사, 부사등이 되며 이는 실제로 큰 의미를 가지지 않을 확률이 높다.

Field-length norm

짧은 필드에 나타나는 term은 긴 필드에 나타나는 동일한 term보다 더 많은 weight를 가진다.
