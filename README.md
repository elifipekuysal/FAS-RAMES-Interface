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

