**1.** query to docker container **cd /usr/share/elasticsearch/bin/**

**2.** elasticsearch-setup-passwords auto -> **save result** to your notepad

**3.** add username/password from elastic, logstash, filebeat, kibana to files config

💡 **Note**: Options config to Kibana Dev Tool

**1.** Config Lifecycle policy to indexes

&nbsp;  PUT mqtt-data**/_settings 
  ```json
  {
    "index": {
      "lifecycle": {
        "name": "Clean-data"
      }
    }
  }
  ```

&nbsp;  **mqtt-data** : Regular expression to map all your indexes

&nbsp;  **Clean-data** : the name of Lifecycle policy
