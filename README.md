# GOALS

The main goal is to define a process and give tools to work on two differents zabbix environments, and also to save zabbix templates in this repository.
This project is using ansible. 


# Working with templates

The workflow is this one :

* Work on test environement (Add templates/updates them ...)
* Test it
* When ok, execute the below command to export templates in json files (one file per template):

```
ansible-playbook -i inventories/test save-tmpl-JSON.yml
```

The templates will be saved in the files folder of the add-templates role.

Becarefull, if there is new templates, edit the ansible role roles/save-tmpl-JSON in order to add the new templates.
At this stage, you have exported templates in json format.

You can save them with git and have a history for your templates. 

Update the templates in production environment by executng this command :

```
ansible-playbook -i inventories/production add-templates.yml
```

The json templates are updated by a task in the save-tpml-JSON role. The taks is "Replace Date field by the one declared in playbook !" and replace a field named date that contains the date of the export. Not welcomed when the goal is to get the history of files. So the date is replaced by {{ version }}

# Go further

Create a variable list to handle the list of templates to save. And so on for the other role. 


