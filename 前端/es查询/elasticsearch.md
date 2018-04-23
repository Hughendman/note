## 模糊查询

```
client.search({
        index: "jw",
        type: "hotel_info",
        body: {
            "query": {
                "fuzzy": {
                    "hotel_name": "南"
                }
            }
        }
    }).then(function (body) {
        hits = body.hits.hits;
        //返回数据
        res.status(200),
            res.json(hits);
    }, function (error) {
        console.trace(error.message);
    });


```

## 精确查询
 
```
client.search({
        index: "jw",
        type: "hotel_info",
        body: {
            query: {
                match: {
                    open_year: 'unknown'
                }
            }
        }
    }).then(function (body) {
        hits = body.hits.hits;
        //返回数据
        res.status(200),
            res.json(hits);
    }, function (error) {
        console.trace(error.message);
    });

```

## 聚合

```
client.search({
        index: "jw",
        type: "hotel_info",
        body: {
            "query": {
                "bool": {
                    "must": [
                        { "fuzzy": { "hotel_name": "南" }},
                        { "fuzzy": { "contact": "025"   }},
                        { "fuzzy": { "address": "山根"   }},
                        { "term": { "city_name": ""   }},
                        { "term": { "province_name": ""   }}
                    ]
                }
            }
        }
    }).then(function (body) {
        hits = body.hits.hits;
        //返回数据
        res.status(200),
            res.json(hits);
    }, function (error) {
        console.trace(error.message);
    });

{
    "query": {
        "bool": {
            "must": [
                {
                    "match": {
                        "hotel_name": {
                            "query": "肯定连锁酒店(南京浦口紫金店)",
                            "fuzziness": "AUTO",
                            "operator": "and"
                        }
                    }
                },
                {
                    "match": {
                        "address": {
                            "query": "浦滨路88号",
                            "fuzziness": "AUTO",
                            "operator": "and"
                        }
                    }
                },
                {
                    "match": {
                        "contact": {
                            "query": "025-58883788",
                            "fuzziness": "AUTO",
                            "operator": "and"
                        }
                    }
                },
                {
                    "match": {
                        "province_name": {
                            "query": "江苏"
                        }
                    }
                },{
                    "match": {
                        "city_name": {
                            "query": "南京"
                        }
                    }
                }
            ]
        }
    }
}


```
