# ControlsInsight API v1.0 (beta)
## Overview
Rapid7's **controlsinsight**, hereafter **controls**insight or simply **controls**,

The **controls**insight API v1.0 allow developers to utilize information about security controls, configurations, threats, and more from **controls**. 

This documentation includes custom Curl examples and Ruby examples using the Ruby API client (ipwnstuff/controls.rb).

Apiary.io also adds example requests in other languages, though they aren't supported tested them.

To see advanced usage in Ruby read the [Ruby client documentation here](http://www.rubydoc.info/github/rapid7/controlsinsight.rb).

## API Reference
See the [API reference page](#api_reference) for more information.

```json
{
  "applicableAssetsUrl": "https://nexpose.local:3780/insight/controls/api/guidance/{guidance}/applicable_assets{?page,per_page,sort}",
  "assessmentsUrl": "https://nexpose.local:3780/insight/controls/api/assessments{/assessment_id}",
  "assetSearchUrl": "https://nexpose.local:3780/insight/controls/api/assets/search{?query,page,per_page,sort}",
  "assetsUrl": "https://nexpose.local:3780/insight/controls/api/assets{/asset_uuid}{?page,per_page,sort}",
  "configurationPrioritizedGuidanceUrl": "https://nexpose.local:3780/insight/controls/api/configurations/{configuration}/prioritized_guidance",
  "configurationTrendUrl": "https://nexpose.local:3780/insight/controls/api/configurations/{configuration}/trend",
  "configurationsUrl": "https://nexpose.local:3780/insight/controls/api/configurations{/configuration}",
  "guidanceUrl": "https://nexpose.local:3780/insight/controls/api/guidance/{guidance}",
  "misconfiguredAssetsUrl": "https://nexpose.local:3780/insight/controls/api/configurations/{configuration}/misconfigured_assets{?page,per_page,sort}",
  "securityControlConfigurationsUrl": "https://nexpose.local:3780/insight/controls/api/security_controls/{security_control}/configurations",
  "securityControlCoverageUrl": "https://nexpose.local:3780/insight/controls/api/coverage/security_controls{/security_control}",
  "securityControlPrioritizedGuidanceUrl": "https://nexpose.local:3780/insight/controls/api/security_controls/{security_control}/prioritized_guidance",
  "securityControlsUrl": "https://nexpose.local:3780/insight/controls/api/security_controls{/security_control}",
  "threatAssetsUrl": "https://nexpose.local:3780/insight/controls/api/threats/{threat}/assets{?page,per_page,sort}",
  "threatGuidanceUrl": "https://nexpose.local:3780/insight/controls/api/threats/{threat}/guidance",
  "threatPrioritizedGuidanceUrl": "https://nexpose.local:3780/insight/controls/api/threats/{threat}/prioritized_guidance",
  "threatThreatVectorsUrl": "https://nexpose.local:3780/insight/controls/api/threats/{threat}/threat_vectors",
  "threatTrendUrl": "https://nexpose.local:3780/insight/controls/api/threats/{threat}/trend",
  "threatVectorPrioritizedGuidanceUrl": "https://nexpose.local:3780/insight/controls/api/threat_vectors/{threat_vector}/prioritized_guidance",
  "threatVectorSecurityControlsUrl": "https://nexpose.local:3780/insight/controls/api/threat_vectors/{threat_vector}/security_controls",
  "threatVectorTrendUrl": "https://nexpose.local:3780/insight/controls/api/threat_vectors/{threat_vector}/trend",
  "threatVectorsUrl": "https://nexpose.local:3780/insight/controls/api/threat_vectors{/threat_vector}",
  "threatsUrl": "https://nexpose.local:3780/insight/controls/api/threats{/threat}",
  "uncoveredAssetsUrl": "https://nexpose.local:3780/insight/controls/api/security_controls/{security_control}/uncovered_assets{?page,per_page,sort}",
  "undefendedAssetsUrl": "https://nexpose.local:3780/insight/controls/api/threat_vectors/{threat_vector}/undefended_assets{?page,per_page,sort}"
}
```

## Authentication
You must authenticate using HTTP Basic Auth when making any of the API requests.

### Curl
See the cURL man pages on how to authenticate.

```bash
# Use -k to allow a self-signed certificate
curl --user admin:password https://nexpose.local:3780/insight/controls/api/1.0
```

### Ruby
```ruby
# Allow connections to Nexpose's self-signed cert
Controls.middleware.ssl[:verify] = false

Controls.login 'admin', 'password'

# Return the API reference for the current API version
Controls.get '/'
```

## Authentication via a `.netrc` file
### Curl
```bash
# Use -k to allow a self-signed certificate
curl -H 'Accept: application/json' --netrc-file ~/.rapid7_netrc  -ik \
https://nexpose.local:3780/insight/controls/api/1.0
```

### Ruby
On the command line run:
```bash
gem install netrc
irb -r controls
```

Once you open IRB run:
```ruby
# Allow connections to Nexpose's self-signed cert
Controls.middleware.ssl[:verify] = false

client = Controls::Client.new({
    :api_endpoint => 'https://nexpose.local:3780/insight/controls/api/1.0',
    :web_endpoint => 'https://nexpose.local:3780/insight/controls',
    :netrc => true,
    :netrc_file => '~/.rapid7_netrc'
})
```

**NOTE**: The **controls** Ruby client doesn't enable or install netrc support by default. You must follow the preceding instructions to enable it.
## Status & Error Codes
### Success
<table>
<tr><th>Status Code</th><th>Status</th><th>Description</th></tr>
<tr><td>200</td><td>OK</td><td>The request was successful (includes a hash/array for the requested resource)</td></tr>
</table>

### Failure
<table>
<tr><th>Status Code</th><th>Status</th><th>Description</th></tr>
<tr><td>401</td><td>Unauthorized</td><td>The request didn't contain any information for authentication</td></tr>
<tr><td>403</td><td>Bad Request</td><td>The query parameters you supplied were invalid</td></tr>
<tr><td>404</td><td>Not Found</td><td>The resource(s) you requested couldn't be found (returns an error message)</td></tr>
</table>

## Error JSON
### Example
```json
{
    "status": 404,
    "messsage": "The resource x could not be found."
}
```
