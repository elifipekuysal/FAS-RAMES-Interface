# RAMES-Interface
Before testing the interfaces, please download the exemplar and follow the [instructions of the exemplar](https://zenodo.org/doi/10.5281/zenodo.10400820)
The six interfaces of the RAMES: 
<ol>
  <li>/monitor(GET): Returns a JSON object with a list of values of everything monitorable about the exemplar. For example, this could include the response time of requests for an exemplar of a web server.</li>
  <li>/monitor_schema(GET): Returns the JSON schema of the JSON object returned by the "monitor" endpoint.</li>
  <li>/execute(POST): Executes an adaptation of the exemplar. A JSON object (likely originating from /adaptation_options) is included in the body of this HTTP request, specifying the adaptation you'd like to enact.</li>
  <li>/execute_schema(GET): Returns the JSON schema of the JSON object returned by the "execute" endpoint.</li>
  <li>/adaptation_option(GET)s: Returns a JSON object with the adaptation options/adaptation space, these are the configurable aspects of the exemplar/system</li>
  <li>/adaptation_options_schema (GET): Returns the JSON schema of the JSON object returned by the "adaptation_options" endpoint.</li>
</ol> 

Here are some examples of test if the exemplar is running correctly:
(Before testing the interfaces, please download the exemplar and follow the [instructions of the exemplar](https://zenodo.org/doi/10.5281/zenodo.10400820), and check the port of each service)


load balance weight:

```bash
 curl -X POST  'http://localhost:55012/rest/changeLBWeights' -H 'Content-Type: application/json' -d '{ "serviceId": "ORDERING-SERVICE","newWeights": {"ordering-service@sefa-ordering-service-36057:36057": 0.75,"ordering-service@sefa-ordering-service:58086":0.25}, "instancesToRemoveWeightOf": [] }'
```

change property:

```bash
curl -X POST 'http://localhost:55012/rest/changeProperty' -H 'Content-Type: application/json' -d '{"serviceName": "ORDERING-SERVICE", "propertyName": "", "value": ""}'
```

removeInstance:

```bash
curl -X POST  'http://localhost:55011/rest/removeInstance' -H 'Content-Type: application/json' -d '{"serviceImplementationName": "ordering-service","address":"sefa-ordering-service", "port":36057 }' 
```

addInstances:

```
bashcurl -X POST  'http://localhost:55011/rest/addInstances' -H 'Content-Type: application/json' -d '{"serviceImplementationName": "ordering-service","numberOfInstances": 1 }' 
```

When you try to test the interface: /changeLBWeights and if the log shows a git problem, you can follow the steps below to solve the problem:

```jsx
# Connect to the container
docker exec -it sefa-config-manager /bin/sh

apt-get update
apt-get install -y git

cd /tmp/config-server*
git checkout main
git branch --set-upstream-to=origin/main main
```