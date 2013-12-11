# Security Controls

## GET /api/security_controls
This endpoint returns a list of security control objects with its name and enabled state.

### Example
The following URL 
https://nexpose.local:3780/insight/controls/api/security_controls
results in the following:-

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
https://nexpose.local:3780/insight/controls/api/security_controls/code-execution-prevention
results in the following:-

```json
    {
       "enabled": true,
       "name": "code-execution-prevention"
    }
```

## PUT /api/security_controls
This endpoint allows list of controls to be selected or deselected 

### Example

Let's select `desktops-with-email-attachment-filtering-enabled`,`desktops-with-up-to-date-high-risk-applications` and deselect `code-execution-prevention`. To see the change, let us do a GET Request on all the security controls

i.e. https://nexpose.local:3780/insight/controls/api/security_controls
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
    {
    	"enabled": false,
    	"name": "desktops-with-email-attachment-filtering-enabled"
    }    	
]
```
``NOTE``: Always at least on control must be selected.

## PUT /api/security_controls/{security_control}
This Endpoints allows a single security control selected or deselected 

### Example

Let's select `code-execution-prevention control`. To see the change, let us do a GET Request on the security control

i.e. https://nexpose.local:3780/insight/controls/api/security_controls/code-execution-prevention

```json
    {
        "enabled": true,
        "name": "code-execution-prevention"
    }
```
