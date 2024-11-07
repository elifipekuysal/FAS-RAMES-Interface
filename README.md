# RAMSES-Interface
Before testing the interfaces, please download the exemplar and follow the [instructions of the exemplar](https://zenodo.org/doi/10.5281/zenodo.10400820)
Here are some examples of test if the exemplar is running correctly:

Before you test the /changeLBWeights interface, make sure the service has more than one instance running. For example, for the order-service,you need at least two instances running. 

addInstances:
find the port of the sefa-instances-manager in your desktop docker or terminal,
change the port 55011 to the sefa-instances-manager port 

```bash
curl -X POST  'http://localhost:55011/rest/addInstances' -H 'Content-Type: application/json' -d '{"serviceImplementationName": "ordering-service","numberOfInstances": 1 }' 
```

removeInstance:
find the port of the sefa-instances-manager in your desktop docker or terminal,
change the port 55011 to the sefa-instances-manager port
```bash
curl -X POST  'http://localhost:55011/rest/removeInstance' -H 'Content-Type: application/json' -d '{"serviceImplementationName": "ordering-service","address":"sefa-ordering-service", "port":36057 }' 
```


load balance weight:
find the port of the sefa-config-manager in your desktop docker or terminal,
change the port 55012 to the sefa-config-manager port
```bash
 curl -X POST  'http://localhost:55012/rest/changeLBWeights' -H 'Content-Type: application/json' -d '{ "serviceId": "ORDERING-SERVICE","newWeights": {"ordering-service@sefa-ordering-service-36057:36057": 0.75,"ordering-service@sefa-ordering-service:58086":0.25}, "instancesToRemoveWeightOf": [] }'
```

change property:
find the port of the sefa-config-manager in your desktop docker or terminal,
change the port 55012 to the sefa-config-manager port
```bash
curl -X POST 'http://localhost:55012/rest/changeProperty' -H 'Content-Type: application/json' -d '{"serviceName": "ORDERING-SERVICE", "propertyName": "", "value": ""}'
```

After testing the interfaces, you can clone this repository to your local, and enter the interface folder.
Replace the port in the api.py,there are three ports: 55010, 55011, 55012. 
* port 55010 is the port of sefa-probe
* port 55011 is the port of sefa-instances-manager
* port 55012 is the port of sefa-config-manager

then run the following command:

```bash
python api.py
```

The six interfaces of the RAMES: 
<ol>
  <li>/monitor(GET): Returns a JSON object with a list of values of everything monitorable about the exemplar. For example, this could include the response time of requests for an exemplar of a web server.</li>
  <li>/monitor_schema(GET): Returns the JSON schema of the JSON object returned by the "monitor" endpoint.</li>
  <li>/execute_schema(GET): Returns the JSON schema of the JSON object returned by the "execute" endpoint.</li>
  <li>/adaptation_option(GET)s: Returns a JSON object with the adaptation options/adaptation space, these are the configurable aspects of the exemplar/system</li>
  <li>/adaptation_options_schema (GET): Returns the JSON schema of the JSON object returned by the "adaptation_options" endpoint.</li>
  <li>/execute(POST): Executes an adaptation of the exemplar. A JSON object (likely originating from /adaptation_options) is included in the body of this HTTP request, specifying the adaptation you'd like to enact.</li>
</ol>


you can test the GET interface by using the browser. For example, you can test the /monitor interface by entering the following URL in the browser:

www.localhost:5000/monitor

For the POST, you need to run it by using the curl command. 
It's a bit complex to test the POST interface, please read the dataclass and execute() in the api.py carefully to understand the data structure of the POST request.
If necessary, you can modify the data structure and execute() of the POST request in the api.py.

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
