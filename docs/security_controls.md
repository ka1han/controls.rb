# Security Controls
## GET /api/security_controls
This endpoint returns a list of security control objects with its name and enabled state.

### Example
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
## PUT /api/security_controls
## PUT /api/security_controls/{security_control}

