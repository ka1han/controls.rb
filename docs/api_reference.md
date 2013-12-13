# API references
## Assessments
* GET /api/assessments
* GET /api/assessments/{assessment_id}

## Assets
* GET /api/assets{?page,per_page,sort}
* GET /api/assets/{asset_uuid}

### Asset search
* GET /api/assets/search{?query,page,per_page,sort}

### Assets by {Configuration,Guidance,Security Control,Threat Vector,Threat}
* GET /api/configurations/{configuration}/misconfigured_assets{?page,per_page,sort}
* GET /api/guidance/{guidance}/applicable_assets{?page,per_page,sort}
* GET /api/security_controls/{security_control}/uncovered_assets{?page,per_page,sort}
* GET /api/threat_vectors/{threat_vector}/undefended_assets{?page,per_page,sort}
* GET /api/threats/{threat}/assets{?page,per_page,sort}

## Configurations
* GET /api/configurations
* GET /api/configurations/{configuration}

### Configurations by Security Control
* GET /api/security_controls/{security_control}/configurations

## Guidance
To retreive an individual guidance you can simply give the guidance name
such as 'enable-uac' (not the human title: 'Enable User Account Control
(UAC)').

* GET /api/guidance/{guidance}

### Guidance by Threat
* GET /api/threats/{threat}/guidance

### Prioritized Guidance by {Configuration,Security Control,Threat Vector,Threat}
* GET /api/configurations/{configuration}/prioritized_guidance
* GET /api/security_controls/{security_control}/prioritized_guidance
* GET /api/threat_vectors/{threat_vector}/prioritized_guidance
* GET /api/threats/{threat}/prioritized_guidance

## Security Controls
* GET /api/security_controls
* GET /api/security_controls/{security_control}

### Security Controls by Threat Vector
* GET /api/threat_vectors/{threat_vector}/security_controls

## Threat Vectors
* GET /api/threat_vectors
* GET /api/threat_vectors/{threat_vector}

### Threat Vectors by Threat
* GET /api/threats/{threat}/threat_vectors

## Threats
* GET /api/threats
* GET /api/threats/{threat}

## Trends
Trends are always tagged along another endpoint since as of yet there
are no trends that don't have a facet.

* GET /api/configurations/{configuration}/trend
* GET /api/threat_vectors/{threat_vector}/trend
* GET /api/threats/{threat}/trend
