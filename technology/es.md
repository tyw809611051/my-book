```
  "settings": {
    "number_of_shards": 5,
    "number_of_replicas": 1,
    "analysis": {
      "analyzer": {
        "my_ngram_analyzer": {
          "type": "custom",
          "tokenizer": "my_ngram_tokenizer",
          "char_filter": [
            "html_strip"
          ],
          "filter": [
            "lowercase"
          ]
        },
        "my_edge_ngram_analyzer": {
          "type": "custom",
          "tokenizer": "my_edge_ngram_tokenizer",
          "char_filter": [
            "html_strip"
          ],
          "filter": [
            "lowercase"
          ]
        }
      },
      "tokenizer": {
        "my_ngram_tokenizer": {
          "type": "nGram",
          "min_gram": "2",
          "max_gram": "50",
          "token_chars": [
            "letter",
            "digit",
            "punctuation"
          ]
        },
        "my_edge_ngram_tokenizer": {
          "type": "edge_ngram",
          "min_gram": "2",
          "max_gram": "50",
          "token_chars": [
            "letter",
            "digit",
            "punctuation"
          ]
        }
      }
    }
  },
  "mappings": {
    "_default_": {
      "_all": {
        "enabled": false
      },
      "dynamic_templates": [
        {
          "param_1": {
            "match": "param_1",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_2": {
            "match": "param_2",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_3": {
            "match": "param_3",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_4": {
            "match": "param_4",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_7": {
            "match": "param_7",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_8": {
            "match": "param_8",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_fields": {
            "match": "param_*",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true
            }
          }
        }
      ],
      "properties": {
        "category_id": {
          "type": "keyword",
          "ignore_above": 4
        },
        "exact_manufacturer_name": {
          "type": "keyword"
        },
        "exact_name": {
          "type": "keyword"
        },
        "exact_norm_no": {
          "type": "keyword"
        },
        "exact_package": {
          "type": "keyword"
        },
        "exact_quality": {
          "type": "keyword"
        },
        "exact_specification_model_no": {
          "type": "keyword"
        },
        "specification_model_no": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "manufacturer_name": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "name": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "norm_no": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "package": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "quality": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "certification": {
          "type": "keyword",
          "index": false
        },
        "cpl_status": {
          "type": "keyword",
          "index": false
        },
        "create_user_id": {
          "type": "long"
        },
        "created_at": {
          "type": "date",
          "index": false,
          "format": "yyyy-MM-dd HH:mm:ss||strict_date_optional_time||epoch_millis"
        },
        "datasheet_id": {
          "type": "long"
        },
        "id": {
          "type": "keyword"
        },
        "insurable": {
          "type": "keyword"
        },
        "invent_status": {
          "type": "keyword",
          "index": false
        },
        "manufacturer_id": {
          "type": "long"
        },
        "new_arrival_id": {
          "type": "long",
          "index": false
        },
        "old_id": {
          "type": "keyword",
          "index": false
        },
        "pid": {
          "type": "long"
        },
        "series_name": {
          "type": "keyword"
        },
        "selected_categories": {
          "type": "keyword"
        },
        "size": {
          "type": "keyword",
          "index": false
        },
        "temperature_high": {
          "type": "keyword"
        },
        "temperature_low": {
          "type": "keyword"
        },
        "updated_at": {
          "type": "date",
          "index": false,
          "format": "yyyy-MM-dd HH:mm:ss||strict_date_optional_time||epoch_millis"
        },
        "verification_status": {
          "type": "keyword",
          "index": false
        },
        "version": {
          "type": "long",
          "index": false
        },
        "weight": {
          "type": "long",
          "index": false
        },
        "data_from": {
          "type": "keyword",
          "index": false
        },
        "data_source_url": {
          "type": "keyword",
          "index": false
        },
        "feature": {
          "type": "keyword",
          "index": false
        },
        "image_url": {
          "type": "keyword",
          "index": false
        },
        "origin": {
          "type": "keyword",
          "index": true
        },
        "replace_model_no": {
          "type": "keyword",
          "index": false
        },
        "typical_customer": {
          "type": "keyword",
          "index": false
        },
        "full_content": {
          "type":    "text"
        }
      }
    }
  }

```

**suggest**
```
	"mappings" : {
		"component" : {
			"_all": {
		        "enabled": false
		    },
			"properties" : {
				"name_suggest" : {
		            "type" : "completion",
		            "analyzer" : "standard",
		            "preserve_separators" : true,
		            "preserve_position_increments" : true,
		            "max_input_length" : 150
		        },
		        "min_suggest" : {
		            "type" : "completion",
		            "analyzer" : "standard",
		            "preserve_separators" : true,
		            "preserve_position_increments" : true,
		            "max_input_length" : 150
		        },
		        "man_suggest" : {
		            "type" : "completion",
		            "analyzer" : "standard",
		            "preserve_separators" : true,
		            "preserve_position_increments" : true,
		            "max_input_length" : 150
		        }
			}
		}
	}
```

**一个index下有多个type，共用一个template**
```
{
  "template": "extend_*",
   "settings": {
    "number_of_shards": 5,
    "number_of_replicas": 1,
    "analysis": {
      "analyzer": {
        "my_ngram_analyzer": {
          "type": "custom",
          "tokenizer": "my_ngram_tokenizer",
          "char_filter": [
            "html_strip"
          ],
          "filter": [
            "lowercase"
          ]
        },
        "my_edge_ngram_analyzer": {
          "type": "custom",
          "tokenizer": "my_edge_ngram_tokenizer",
          "char_filter": [
            "html_strip"
          ],
          "filter": [
            "lowercase"
          ]
        }
      },
      "tokenizer": {
        "my_ngram_tokenizer": {
          "type": "nGram",
          "min_gram": "2",
          "max_gram": "50",
          "token_chars": [
            "letter",
            "digit",
            "punctuation"
          ]
        },
        "my_edge_ngram_tokenizer": {
          "type": "edge_ngram",
          "min_gram": "2",
          "max_gram": "50",
          "token_chars": [
            "letter",
            "digit",
            "punctuation"
          ]
        }
      }
    }
  },
  "mappings": {
    "_default_": {
      "_all": {
        "enabled": false
      },
      "dynamic_templates": [
        {
          "param_1": {
            "match": "param_1",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_2": {
            "match": "param_2",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_3": {
            "match": "param_3",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_4": {
            "match": "param_4",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_7": {
            "match": "param_7",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_8": {
            "match": "param_8",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true,
              "copy_to": "full_content"
            }
          }
        },
        {
          "param_fields": {
            "match": "param_*",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword",
              "index": true
            }
          }
        }
      ],
      "properties": {
        "category_id": {
          "type": "keyword",
          "ignore_above": 4
        },
        "exact_manufacturer_name": {
          "type": "keyword"
        },
        "exact_name": {
          "type": "keyword"
        },
        "exact_norm_no": {
          "type": "keyword"
        },
        "exact_package": {
          "type": "keyword"
        },
        "exact_quality": {
          "type": "keyword"
        },
        "exact_specification_model_no": {
          "type": "keyword"
        },
        "specification_model_no": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "manufacturer_name": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "name": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "norm_no": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "package": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "quality": {
          "type": "text",
          "store": true,
          "analyzer": "my_ngram_analyzer"
        },
        "certification": {
          "type": "keyword",
          "index": false
        },
        "cpl_status": {
          "type": "keyword",
          "index": false
        },
        "create_user_id": {
          "type": "long"
        },
        "created_at": {
          "type": "date",
          "index": false,
          "format": "yyyy-MM-dd HH:mm:ss||strict_date_optional_time||epoch_millis"
        },
        "datasheet_id": {
          "type": "long"
        },
        "id": {
          "type": "keyword"
        },
        "insurable": {
          "type": "keyword"
        },
        "invent_status": {
          "type": "keyword",
          "index": false
        },
        "manufacturer_id": {
          "type": "long"
        },
        "new_arrival_id": {
          "type": "long",
          "index": false
        },
        "old_id": {
          "type": "keyword",
          "index": false
        },
        "pid": {
          "type": "long"
        },
        "series_name": {
          "type": "keyword"
        },
        "selected_categories": {
          "type": "keyword"
        },
        "size": {
          "type": "keyword",
          "index": false
        },
        "temperature_high": {
          "type": "keyword"
        },
        "temperature_low": {
          "type": "keyword"
        },
        "updated_at": {
          "type": "date",
          "index": false,
          "format": "yyyy-MM-dd HH:mm:ss||strict_date_optional_time||epoch_millis"
        },
        "verification_status": {
          "type": "keyword",
          "index": false
        },
        "version": {
          "type": "long",
          "index": false
        },
        "weight": {
          "type": "long",
          "index": false
        },
        "data_from": {
          "type": "keyword",
          "index": false
        },
        "data_source_url": {
          "type": "keyword",
          "index": false
        },
        "feature": {
          "type": "keyword",
          "index": false
        },
        "image_url": {
          "type": "keyword",
          "index": false
        },
        "origin": {
          "type": "keyword",
          "index": true
        },
        "replace_model_no": {
          "type": "keyword",
          "index": false
        },
        "typical_customer": {
          "type": "keyword",
          "index": false
        },
        "full_content": {
          "type":    "text"
        }
      }
    }
  }
}
}
```