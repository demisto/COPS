# dfir-playbook-spec

This repository contains schema definitions for a DFIR (Digital Forensics Incident Response) Playbook .
The scheme is based on YAML (http://yaml.org/), this is inorder to describe an Incident response runbook (aka. playbook, “use case”) is a written guidance for identifying, containing, eradicating and recovering from cyber security incidents.

Yaml was chosen since it's both human readable and can describe complex nested data structure.

## What is the promise of the DFIR Playbook Spec?
* Open - open sourced , so analysts can create, share and contribute incident response process in same language.
* Semi/Fully automated - since playbook in the incident response world often must have some manual steps, but sometimes can be fully automated.
* Visibility - give the organization members (SOC team , managment) an overview on the incident response process.


Playbook Hierarchy structure:
1. Playbook - the high level process.
2. Task - this is a single step in the process, can represent a script execution or manual step.


