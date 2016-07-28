# dfir-playbook-spec

This repository contains schema definitions for a DFIR (Digital Forensics Incident Response) Playbook .
The scheme is based on YAML (http://yaml.org/), this is inorder to describe an Incident response runbook (aka. playbook, “use case”) is a written guidance for identifying, containing, eradicating and recovering from cyber security incidents.

Yaml was chosen since it's both human readable and can describe complex nested data structure.

## What is the promise of the DFIR Playbook Spec?
* Open - open sourced , so analysts can create, share and contribute incident response process in same language.
* Semi/Fully automated - since playbook in the incident response world often must have some manual steps, but sometimes can be fully automated.
* Visibility - give the organization members (SOC team , managment) an overview on the incident response process.


## Playbook Hierarchy structure:
1. Playbook - the high level process.
2. Task - this is a single step in the process, can represent a script execution or manual step.

## Playbook fields

* id: a unique id of the playbook, usually UUID
* name: playbook name
* description: the purpose of the playbook
* tasks: an (orderd) list of playbook tasks

## Task fields
* id: this is the id of the task inside the playbook, it must by unique in playbook level only
* taskid: this is the global task id, should be unique globaly(usually UUID), needed in order to share task between playbooks * type: on of the three title(represent a new playbook section/header), regular(script or manual task) or condition(to decide what is the next branch/step)
* name: name of the task
* description: the purpose of the task
* script: if this is an automated task, the script to execute for this task
* tags: general tags to add to task
* condition: if this task is condition type, this fields will hold a nested map of string keys that map to branchs(list of tasks), so this task can continue to correct branch according to result of script
* scriptarguments: these are the task inputs, should be a map of string(input name) to string(input value or identifier)
* results: script results that we can propagate to the rest of the playbook execution



