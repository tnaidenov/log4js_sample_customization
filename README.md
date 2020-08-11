# log4js_sample_customization
Sample customization for GlueDesktop logging.
This customization is based on/uses the [logstash Appender (HTTP) for log4js-node](#https://github.com/log4js-node/logstashHTTP) with [Apache License 2.0](#https://github.com/log4js-node/logstashHTTP/blob/master/LICENSE).  

GlueDesktop uses [log4js-node](https://log4js-node.github.io/log4js-node/) for logging but does not include the optional logstash appender.
Using this sample customization allows directing GlueDesktop log messages to logstash/elasticsearch.

## Installation
Download/clone the `node_modules` directory and put it under `GlueDesktop\resources` in your Glue installation directory.  
This includes the logstash appender and some of its required dependencies.

## Configuration
The logger configuration for GlueDesktop is in `GlueDesktop\config\logger.json`, located in the Glue installation directory.

### Add the appender configuration
Under `appenders`, add the configuration for the logstash appender (details in the appender's README [here](#https://github.com/log4js-node/logstashHTTP/blob/master/README.md))

```json
    "appenders": {
        "logstash": {
            "type": "@log4js-node/logstash-http",
            "url": "http://localhost:9200/_bulk",
            "application": "glue-app-log",
            "logType": "application"
        },
        ...
```

### Use the appender
Under `categories`, add/replace the configured `logstash` appender, e.g:  
```json
    "categories": {
        "default": {
            "appenders": ["out", "app", "logstash"],
            "level": "debug"
        },
    ...
```

## Further customization
You can edit the `index.js` file under `node_modules\@log4js-node\logstash-http\lib` to change or (re)format the data saved in elasticsearch, apply filtering, etc.


