# Export ThingWorx projects for source control

The purpose of this project is to automate the exporting of ThingWorx entities for source control into a ThingWorx FileRepository. From there it would be possible to use git to automatically commit changes.

This project contains:
- a file repository entity
- a helper thing 
- a timer

The FileRepository entity has a service called `init` that should be manually called once (invoke it from ThingWorx Composer after you import this project).

The Timer entity raises a Timer event once per minute (configurable).

The Helper entity has two properties, two services and a subscription
The subscription reacts to the Timer event and exports for source control all projects referenced from the `Projects` property of the Helper entity. The subscription eventually invokes the `Export` service.

The `Projects` property is a JSON string that contains a `projects` key which is an array of project names: all projects that would be exported by the subscrption above.



# GIT interaction

There is no direct GIT interaction yet, but the `init` service of the FileRepository entity generates a PowerShell script that could be used to automatically commit exported source.

The idea is that each folder under the FileRepository folder in ThingWorx storage is a local git repository. You need to run a `git init` command in each exported folder before running the PowerShell script.

The PowerShell script commits each minute all changes.

