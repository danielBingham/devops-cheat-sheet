# DevOps / SRE Cheat Sheet
A collection of commands, one liners, and generally helpful things I've come across over the years that I don't want to lose.

## Get all deployments using a secret as an Environment Variable

This will return a list of all deployments currently using a secret through an environment variable.
```bash
kubectl get deployments -o json | jq '.items[] | { name: .metadata.name, secrets: [ .spec.template.spec.containers[]?.env[]?.valueFrom.secretKeyRef.name ] } | select(.secrets[] == "db-uri")'
```
