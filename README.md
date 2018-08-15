# Elasticsearch HTTP Basic User Auth plugin (and its web console)

Elasticsearch user authentication plugin with http basic auth.
This plugin provides user authentication APIs and its web console. 

## Installation 
<pre>
bin/plugin --url https://raw.githubusercontent.com/TomSearch/elasticsearch-http-user-auth/master/jar/http-user-auth-plugin-1.0-SNAPSHOT.jar --install http-user-auth-plugin
</pre>

## Configuration
Add following lines to elasticsearch.yml:
<pre>
http.user.auth.disabled: false
http.user.auth.root.password: rootpassword
</pre>

If you set `http.user.auth.disabled` to `true`, your Elasticsearch instance won't load this plugin.  
`http.user.auth.root.password` is a setting for root user's password literally.  
**Only the root user can access Elasticsearch root APIs (like /_cat, /_cluster) and all indices.**  
Other users can only access their own indices that are specified by an API of this plugin.  

## Append username and password to HTTP requests
The authentication method of this plugin is Basic Authentication. Therefore, you should add your username and password to URL strings. 

For example, you can call "You know, for search" API like this: *http://root:rootpassword@your.elasticsearch.hostname:9200/*

If you're using some other plugins which use Elasticsearch APIs, you may have to set your root password in their configurations.

For example, configs of Marvel and Kibana 4 shold be as below: 

#### Marvel 
elasticsearch.yml:
<pre>
marvel.agent.exporter.es.hosts: ["root:rootpassword@127.0.0.1:9200"]
</pre>

#### Kibana 4
kibana.yml: 
<pre>
elasticsearch_url: "http://root:rootpassword@localhost:9200"
</pre>


## User Management Console

This plugin provides a web console managing users and their own indices. 
<pre>
http://your.elasticsearch.hostname:9200/_plugin/http-user-auth-plugin/index.html
</pre>
