# Security Controls
Lets assume that we have ControlsInsight running in our localhost and on port 8080.
## GET /api/security_controls
This endpoint returns a list of security control objects with its name and enabled state.

### Example
The following URL 
http://localhost:8080/insight/controls/api/security_controls
results in the following result

```json
[
    {
        "enabled": true,
        "name": "desktops-with-up-to-date-high-risk-applications"
    },
    {
        "enabled": true,
        "name": "code-execution-prevention"
    },
    ...       
    {
    	"enabled": false,
    	"name": "desktops-with-email-attachment-filtering-enabled"
    }    	
]
```
## GET /api/security_controls/{security_control}
This endpoint returns a security control object with its name and enabled state

### Example
The following URL
http://localhost:8080/insight/controls/api/security_controls/code-execution-prevention
results in the following result

```json
    {
        "enabled": true,
        "name": "code-execution-prevention"
    }
```

## PUT /api/security_controls
This Endpoints allows a list of controls selected or deselected in the UI to be saved into the database

### Example

Let's select desktops-with-email-attachment-filtering-enabled, desktops-with-up-to-date-high-risk-applications and deselect code-execution-prevention. When we click save  desktops-with-email-attachment-filtering-enabled, desktops-with-up-to-date-high-risk-applications gets enabled and code-execution prevention control gets disabled

To see this change, let us do a GET Request on all the security controls

i.e. http://localhost:8080/insight/controls/api/security_controls
Now we get the following:-

```json
[
    {
        "enabled": true,
        "name": "desktops-with-up-to-date-high-risk-applications"
    },
    {
        "enabled": true,
        "name": "code-execution-prevention"
    },
	...       
    {
    	"enabled": false,
    	"name": "desktops-with-email-attachment-filtering-enabled"
    }    	
]
```
Note: Always at least on control must be selected.

## PUT /api/security_controls/{security_control}
This Endpoints allows a single security control selected or deselected in the UI to be saved into the database

### Example

Let's select code-execution-prevention control and click save. 

To see this change, let us do a GET Request on all the security control

i.e. http://localhost:8080/insight/controls/api/security_controls/code-execution-prevention

```json
    {
        "enabled": true,
        "name": "code-execution-prevention"
    }
```



