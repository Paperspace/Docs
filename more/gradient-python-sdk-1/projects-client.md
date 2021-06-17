# Projects Client

### Importing

```python
from gradient import ProjectsClient
api_key='YOUR_API_KEY'

projects_client = ProjectsClient(api_key)
```

### Creating Projects

```python
project_id = projects_client.create('your-project-name')
print("project_id: "+project_id)
```

```
project_id: prg8149k1
```

This returns the project ID of the newly created project. Saving this is useful to pass in as input or filter for other queries you make.

### Listing Projects

```python
projects_list = projects_client.list()
for project in project_list:
       print("project_id: "+project.id +" project_name: "+ project.name)   
```

```text
project_id: prg8149k1 project_name: 'your-project-name'
```

### Projects Object

```text
class Project(builtins.object)
 |  Project class
 |  
 |  :param str id:
 |  :param str name:
 |  :param str repository_name:
 |  :param str repository_url:
 |  :param datetime created:
```

### Getting Help

If you are ever stuck, you can call help on any ProjectsClient object or function

```text
help(ProjectsClient.list)

Help on function list in module gradient.api_sdk.clients.project_client:

list(self)
    Get list of your projects
    
    *EXAMPLE*::
    
        gradient projects list
    
    *EXAMPLE RETURN*::
    
        +-----------+------------------+------------+----------------------------+
        | ID        | Name             | Repository | Created                    |
        +-----------+------------------+------------+----------------------------+
        | project-id| <name-of-project>| None       | 2019-06-28 10:38:57.874000 |
        | project-id| <name-of-project>| None       | 2019-07-17 13:17:34.493000 |
        | project-id| <name-of-project>| None       | 2019-07-17 13:21:12.770000 |
        | project-id| <name-of-project>| None       | 2019-07-29 09:26:49.105000 |
        +-----------+------------------+------------+----------------------------+
    
    in sdk::
    
        from gradient.api_sdk.clients import ProjectsClient
    
        api_key = 'your-api-key'
        projects_client = ProjectsClient(api_key)
    
        projects_list = projects_client.list()
    
        for project in project_list:
            print(project)
```

