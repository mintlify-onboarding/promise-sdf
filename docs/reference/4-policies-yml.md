---
sidebar_position: 4
---

# Policy Schema

<!-- 
## Examples
### Individual Policies
#### Data Classification
#### Roles
#### Purposes
#### Storage seperation
### Composite Policies
### A Company Privacy Policy
### GDPR
### HIPPA

## The Schema Definition -->
Policies are rigidly defined a json schema
**[policy.schema.json](
https://github.com/promise-labs/sdf-cli/blob/main/sdf-schemas/policy.schema.json)**.
Here is its quintessence:


### Root Element: `policy`
JSON schema for SDF policy files -- note that a policy should have only one root element which is either allow or deny.
```yml
policy:
  deny: deny_clause
  allow: allow_clause
```
### Nested Element: `deny_clause`
Deny access when these labels are present.
```yaml
  # A list of store labels [defined in 'store.classifier.yml']
  store: array of string
  # A list of role labels [defined in 'role.classifier.yml']
  role: array of string
  # A list of purpose labels [defined in 'purpose.classifier.yml']
  purpose: array of string
  # A list of data classifier labels [defined in 'data.classifier.yml']
  data: array of string
  # EXCEPT for these conditions...
  except: array of 
    required allow: allow_clause
```
### Nested Element: `allow_clause`
Allow access when these labels are present.
```yaml
  # A list of store labels [defined in 'store.classifier.yml']
  store: array of string
  # A list of role labels [defined in 'role.classifier.yml']
  role: array of string
  # A list of purpose labels [defined in 'purpose.classifier.yml']
  purpose: array of string
  # A list of data classifier labels [defined in 'data.classifier.yml']
  data: array of string
  # EXCEPT for these conditions...
  except: array of 
    required deny: deny_clause
```

