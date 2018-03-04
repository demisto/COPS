# COPS - Collaborative Open Playbook Standard

This repository contains schema definitions for a DFIR (Digital Forensics Incident Response) Playbook.
The scheme is based on YAML (http://yaml.org/), and describes an incident response runbook (aka. playbook, “use case”) that is a written guidance for identifying, containing, eradicating and recovering from cyber security incidents.

Yaml was chosen since it's both human readable and can describe complex nested data structure, we use YAML version 1.2.

## What is the promise of the DFIR Playbook Spec?
* **Open** - open sourced, so analysts can create, share and contribute incident response process in same language.
* **Semi/Fully automated** - since playbook in the incident response world often must have some manual steps, but sometimes can be fully automated.
* **Visibility** - give the organization members (SOC team, management) an overview on the incident response process.

## Version
This is version 0.1 of the spec

## Playbook Hierarchy structure:
1. Playbook - the high level process.
2. Task - this is a single step in the process, can represent a script execution or manual step.

## Playbook fields

* **id**: a unique id of the playbook, usually UUID
* **name**: playbook name
* **description**: the purpose of the playbook
* **tasks**: an (orderd) list of playbook tasks

## Task fields
* **id**: this is the id of the task inside the playbook, it must by unique in playbook level only
* **taskid**: this is the global task id, should be unique globally (usually UUID), needed in order to share task between playbooks
* **type**: one of the three title (represent a new playbook section/header), regular (script or manual task) or condition (to decide what is the next branch/step)
* **name**: name of the task
* **description**: the purpose of the task
* **script**: if this is an automated task, the script to execute for this task
* **tags**: general tags to add to task
* **condition**: if this task is condition type, this fields will hold a nested map of string keys that map to branch's (list of tasks), so this task can continue to correct branch according to result of script
* **scriptarguments**: these are the task inputs, should be a map of string (input name) to array (input value or identifier)
* **results**: script results that we can propagate to the rest of the playbook execution

### Example playbook Yaml:

``` yaml
id: ca1822c4-6208-41b3-81c5-ca1e11a48901
name: HelloWorld-Playbook
description: Just a hello world example playbook
tasks:
- id: "1"
  taskid: 6121dfe5-1d26-4fb5-84b2-c03b71c14fb3
  type: condition
  task:
    id: 6121dfe5-1d26-4fb5-84b2-c03b71c14fb3
    name: Are you a DFIR lover?
    description: This will decide the print msg according to person
    script: IsDFIRPerson
  condition:
    "No":
    - id: "2"
      taskid: 9418fbce-5113-4e7e-8747-c6f0f75fd9f7
      type: regular
      task:
        id: 9418fbce-5113-4e7e-8747-c6f0f75fd9f7
        name: manual task
        description: Write hello world using a pen
    "Yes":
    - id: "3"
      taskid: 04b38429-d8b8-4dc3-866a-bddec43580c5
      type: regular
      task:
        id: 04b38429-d8b8-4dc3-866a-bddec43580c5
        name: Hello
        description: Print Hello DFIR !
        script: print
      scriptarguments:
        msg: Hello DFIR !
      results:
      - printOutput
- id: "4"
  taskid: a06f606e-ef14-4f8e-8ad8-f1d6e6caab84
  type: title
  task:
    id: a06f606e-ef14-4f8e-8ad8-f1d6e6caab84
    name: End of Playbook
```
![Example Playbook Image](/images/example-playbook.png)

This is of course a sample (and simple example) just to show an overview of the scheme.
For real DFIR playbooks look at the [Demisto content repo](https://github.com/demisto/content).

Feel free to contribute by providing feedback, creating new DFIR playbooks, or using the spec in your security product, contact using issues of this GitHub repo.
