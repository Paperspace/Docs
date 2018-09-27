# Create a Project

## About

A project is simply a directory or name for a set of related files and jobs. 

## Initializing a New Project

If you do not initialize a particular name or directory, job commands will be given a project name corresponding to the current directory name. 

```
$ paperspace project init
```

This creates a `.ps_project/config.json` file in the current directory to cache information about the project, such as the name, or the last job created.

