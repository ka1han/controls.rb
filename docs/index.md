# ControlsInsight API v1.0 (beta)
## Overview
Rapid7's **controlsinsight**, hereafter **controls**insight or simply **controls**,

The **controls**insight API v1.0 allow developers to utilize information about security controls, configurations, threats, and more from **controls**. 

This documentation includes custom Curl examples and Ruby examples using the Ruby API client (ipwnstuff/controls.rb).

Apiary.io also adds example requests in other languages, though they aren't supported tested them.

To see advanced usage in Ruby read the [Ruby client documentation here](http://www.rubydoc.info/github/rapid7/controlsinsight.rb).

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

## API endpoints
### Assessments
* GET /api/assessments
* GET /api/assessments/{assessment_id}

### Assets
* GET /api/assets{?page,per_page,sort}
* GET /api/assets/{asset_uuid}

#### Asset search
* GET /api/assets/search{?query,page,per_page,sort}

#### Assets by {Configuration,Guidance,Security Control,Threat Vector,Threat}
* GET /api/configurations/{configuration}/misconfigured_assets{?page,per_page,sort}
* GET /api/guidance/{guidance}/applicable_assets{?page,per_page,sort}
* GET /api/security_controls/{security_control}/uncovered_assets{?page,per_page,sort}
* GET /api/threat_vectors/{threat_vector}/undefended_assets{?page,per_page,sort}
* GET /api/threats/{threat}/assets{?page,per_page,sort}

### Configurations
* GET /api/configurations
* GET /api/configurations/{configuration}

#### Configurations by Security Control
* GET /api/security_controls/{security_control}/configurations

### Guidance
To retreive an individual guidance you can simply give the guidance name
such as 'enable-uac' (not the human title: 'Enable User Account Control
(UAC)').

* GET /api/guidance/{guidance}

#### Guidance by Threat
* GET /api/threats/{threat}/guidance

#### Prioritized Guidance by {Configuration,Security Control,Threat Vector,Threat}
* GET /api/configurations/{configuration}/prioritized_guidance
* GET /api/security_controls/{security_control}/prioritized_guidance
* GET /api/threat_vectors/{threat_vector}/prioritized_guidance
* GET /api/threats/{threat}/prioritized_guidance

### Security Controls
* GET /api/security_controls
* GET /api/security_controls/{security_control}

#### Security Controls by Threat Vector
* GET /api/threat_vectors/{threat_vector}/security_controls

### Threat Vectors
* GET /api/threat_vectors
* GET /api/threat_vectors/{threat_vector}

#### Threat Vectors by Threat
* GET /api/threats/{threat}/threat_vectors

### Threats
* GET /api/threats
* GET /api/threats/{threat}

### Trends
Trends are always tagged along another endpoint since as of yet there
are no trends that don't have a facet.

* GET /api/configurations/{configuration}/trend
* GET /api/threat_vectors/{threat_vector}/trend
* GET /api/threats/{threat}/trend
