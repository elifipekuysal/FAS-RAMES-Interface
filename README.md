# RAMES-Interface
Before testing the interfaces, please download the exemplar and follow the [instructions of the exemplar](https://zenodo.org/doi/10.5281/zenodo.10400820)
The six interfaces of the RAMES: 
<ol>
  <li>/monitor: Returns a JSON object with a list of values of everything monitorable about the exemplar. For example, this could include the response time of requests for an exemplar of a web server.</li>
  <li>/monitor_schema</li>
  <li>/executeExecutes an adaptation of the exemplar. A JSON object (likely originating from /adaptation_options) is included in the body of this HTTP request, specifying the adaptation you'd like to enact.</li>
  <li>/execute_schema</li>
  <li>/adaptation_options</li>
  <li>/adaptation_options_schema</li>
</ol> 

