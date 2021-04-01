# Export ThingWorx projects for source control

This project contains a file repository entity, a helper thing and a timer.

The FileRepository entity has a service called `init` that should be called once (invoke it manually from ThingWorx Composer).

The timer raises a Timer event once per minute (configurable).

The Helper entity has two properties, two services and a subscription: the latter subscribes to the Timer event and exports for source control all projects referenced from the `Projects` property. It invokes the `Export` service in order to do so.

The `Projects` property is a JSON string that contains a `projects` key which is an array of project names: all projects that would be exported by the subscrption above.



# GIT interaction

There is no direct GIT interaction yet, but the `init` service of the FileRepository entity generates a PowerShell script that could be used to commit once per minute.

The idea is that each folder under the FileRepository folder in ThingWorx storage should receive a `git init` command so that each minute all changes to a ThingWorx project would be saved in git history.

