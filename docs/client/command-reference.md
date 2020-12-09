<h3 id="ctm-cancel-pipelineinstance" title="Permalink">ctm-cancel-pipelineinstance&nbsp;<a href="#ctm-cancel-pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>


Cancels a processing Pipeline Instance.
    
    Sets all Processing or Pending statuses to 'Canceled'.

Returns success or failure.

    REQUIRED PARAMETERS
        -i,--pi                  Name or ID of a Pipeline Instance.

#### Associated API: **cancel\_pipelineinstance**

Cancel a running Pipeline Instance.

All Pending or Processing statuses will be set to Canceled.

Required Arguments:

* `pi` - The Name or ID of a Pipeline Instance.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-complete-activity" title="Permalink">ctm-complete-activity&nbsp;<a href="#ctm-complete-activity" style="display: margin-left: 1em;">&para;</a></h3>


Given a Package Name, Revision (or Full Version), and Activity Name - will complete that Activity with either 'success' or 'failure'.

Returns: `success` on success, errors otherwise.

    REQUIRED PARAMETERS
        -p,--package             Name of Package
        -h,--phase               Phase containing the Activity/Control to
                                      override..
        -a,--activity            Name of Activity
    OPTIONAL PARAMETERS
        -n,--notes               Notes to be placed on the Activity.
        -r,--revision            Revision of Package containing the
                                      Control. (Takes precedence over
                                      "fullversion" if both are provided.)
        -f,--full_version        Full Version label of the Package
                                      containing the Control.
        --forcewith              Force the completion.  (Will mark ALL
                                      Controls with the provided value - must be
                                      `pass` or `fail`.)
        --failure                Mark the Activity as a Failure. (Will
                                      default to `success` if omitted.)

#### Associated API: **complete\_activity**

Given a Phase, Package Name, Revision (or Full Version), and Activity Name - will complete that Activity with either 'success' or 'failure'.

Required Arguments:

* `package` - Name of the Package to promote to a progression Phase.
* `revision` - Revision number of a Package to promote, takes precedence over `full_version`.
* `full_version` - Full Version of package to promote, optional alternative selector to `revision`.
* `phase` - Name of the Phase containing the Activity to complete.
* `activity` - Name of the Activity to complete.

Optional Arguments:

* `notes` - Notes to be attached to the Activity. (May be configured to be required.)
* `failure` - Mark the Activity as a 'failure'.  (`success` if omitted.)
* `forcewith` - Force completion by setting all Controls to `pass` or `fail`.

Returns: `success` on success, errors otherwise.

<h3 id="ctm-configure-plugin" title="Permalink">ctm-configure-plugin&nbsp;<a href="#ctm-configure-plugin" style="display: margin-left: 1em;">&para;</a></h3>


Configures the details of a specific plugin from a JSON document.

    WARNING: this command will OVERWRITE the existing plugin configuration!

    USE WITH CAUTION.


    REQUIRED PARAMETERS
        -b,--backupfile          A JSON document formatted as a single
                                      Plugin Configuration.

#### Associated API: **configure\_plugin**

Configure a specific Flow Plugin.

Required Arguments:

* `plugin` - JSON object formatted as a valid config for the specified plugin.

> The following keys will be encrypted if provided: `token`, `password`.

Returns: success or error.

<h3 id="ctm-configure-plugins" title="Permalink">ctm-configure-plugins&nbsp;<a href="#ctm-configure-plugins" style="display: margin-left: 1em;">&para;</a></h3>


Configures the details of multiple plugins from a JSON document.
    
    WARNING: this command will OVERWRITE any existing plugin configuration!
    
    USE WITH CAUTION.


    REQUIRED PARAMETERS
        -b,--backupfile          A JSON document formatted as a list of
                                      Plugin Configurations.

#### Associated API: **configure\_plugins**


<h3 id="ctm-copy-project" title="Permalink">ctm-copy-project&nbsp;<a href="#ctm-copy-project" style="display: margin-left: 1em;">&para;</a></h3>


Copy a Project object.

    REQUIRED PARAMETERS
        -p,--project             Value can be either a Project ID or Name.
        -n,--newname             A name for the new Project.
**Examples**

    ctm-copy-project -p "ProjectName"


#### Associated API: **copy\_project**

Copy a Project.

Required Arguments:

* `project` - the id or name of a Project.
* `newname` - a name for the new Project.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-create-asset" title="Permalink">ctm-create-asset&nbsp;<a href="#ctm-create-asset" style="display: margin-left: 1em;">&para;</a></h3>


Creates a new fixed address Asset.

    REQUIRED PARAMETERS
        -n,--name                A name for the new Asset.
    OPTIONAL PARAMETERS
        -s,--status              Status, either "Active" or "Inactive".
                                      ("Active" if omitted.)
        -a,--address             Network address of the Asset.
        -t,--port                Service port of the Asset.
        -d,--db_name             A database name.
        -u,--user                A User ID.
        -p,--password            A Password.
        -c,--shared_credential   A Shared Credential.
        --conn_string            A full connection string. (Not typical.)
**Examples**

    ctm-create-asset -n "Test 123" -s "Active" -a "10.10.2.2" -d "test02" -t "1433" -u "appuser" -p "passw0rd"


#### Associated API: **create\_asset**

Creates an Asset.

Required Arguments:

* name - a name for the new Asset.

Optional Arguments:

* `status` - either 'Active' or 'Inactive'. ('Active' if omitted.)
* `db_name` - a Database name.
* `address` - the network address of the Asset.
* `port` - a service port for the Address.
* `conn_string` - some Assets make their connections via an explicit connection string.
* `user` - a User ID to associate with this Asset.
* `password` - a Password to associate with this Asset.
* `shared_credential` - the name of a Shared Credential to use.

**Regarding Credentials:**

Credentials are optional on an Asset, however if provided there are rules.
Explicit details can be associated with *only this Asset*, or a Shared Credential can be specified.

The minimum required to create a LOCAL set of credentials on this Asset are:

* `user` - a User ID for the Credential
* `password` - a Password for the Credential

To specify a Shared Credential, provide the `shared_credential` argument, which is the name of an existing Credential.

Returns: An [Asset Object](api-response-objects#asset).

<h3 id="ctm-create-credential" title="Permalink">ctm-create-credential&nbsp;<a href="#ctm-create-credential" style="display: margin-left: 1em;">&para;</a></h3>


Creates a new set of Shared Credentials that can be used to log into other systems.

    REQUIRED PARAMETERS
        -n,--name                A name for the new Credential, must be
                                      unique.
        -d,--description         Credential description or long name.
        -u,--username            The user/login name.
        -p,--password            The password/privatekey.
    OPTIONAL PARAMETERS
        -o,--domain              An optional domain name for the
                                      credential.
        -v,--privileged          Additional password required to put
                                      certain Cisco IOS devices into
                                      "privileged" mode.
**Examples**

    ctm-create-credential -n "adminuser" -d "Administrator User" -u "root" -p "passw0rd"


#### Associated API: **create\_credential**

Creates a new Shared Credential.

> Only a 'Developer' can create Credentials.

Required Arguments:

* `name` - The full name of the user.
* `username` - A login name for the user.
* `password` - Password for the user. If password is not provided, a random password will be generated.

Optional Arguments:

* `description` - Description of the Credential.
* `domain` - A domain for the Credential.

Returns: A [Credential Object](api-response-objects#credential).

<h3 id="ctm-create-pipeline" title="Permalink">ctm-create-pipeline&nbsp;<a href="#ctm-create-pipeline" style="display: margin-left: 1em;">&para;</a></h3>


Creates a Pipeline definition from a JSON document.

Returns a Pipeline Object.

    REQUIRED PARAMETERS
        -t,--templatefile        A JSON document formatted as a CSK
                                      Pipeline definition.

#### Associated API: **create\_pipeline**

Create a Pipeline Definition.

Required Arguments:

* `template` - A JSON document formatted as a CSK Pipeline Definition.

Returns: A [Pipeline Definition Object](api-response-objects#pipeline-definition).

<h3 id="ctm-create-project" title="Permalink">ctm-create-project&nbsp;<a href="#ctm-create-project" style="display: margin-left: 1em;">&para;</a></h3>


Creates a Project.

Returns a Project Object.

    REQUIRED PARAMETERS
        -n,--name                A name for the Project.
        -t,--team                Team which the project should belong to
    OPTIONAL PARAMETERS
        -d,--description         A description for the Project.

#### Associated API: **create\_project**

Create a Project.

Required Arguments:

* `name` - Name of the Project.
* `team` - Team which the Project belongs to.

Returns: A [Project Object](api-response-objects#project).

<h3 id="ctm-create-tag" title="Permalink">ctm-create-tag&nbsp;<a href="#ctm-create-tag" style="display: margin-left: 1em;">&para;</a></h3>


Creates a new Tag to be used to associate objects with one another.

    REQUIRED PARAMETERS
        -n,--name                The name of the new Tag.  (AlphaNumeric
                                      ONLY. Cannot contain spaces, punctuation
                                      or special characters.)
    OPTIONAL PARAMETERS
        -d,--description         Tag description.
**Examples**

    ctm-create-tag -n "staging01" -d "staging environment 1"


#### Associated API: **create\_tag**

Creates a new Tag for grouping Users.

Required Arguments:

* `name` - The name of the new Tag.  (AlphaNumeric ONLY. Cannot contain spaces, punctuation or special characters.)

Optional Arguments:

* `description` - Describe the Tag.

Returns: The new [Tag Object](api-response-objects#tag) if successful, error message on failure.
    
<h3 id="ctm-create-task" title="Permalink">ctm-create-task&nbsp;<a href="#ctm-create-task" style="display: margin-left: 1em;">&para;</a></h3>


Creates a new blank Task object.

    REQUIRED PARAMETERS
        -n,--name                A name for the new Task.
        -t,--team                Team which the task belongs to
    OPTIONAL PARAMETERS
        -d,--desc                A description of the new Task.
        -c,--code                A code for the new Task.
**Examples**

    ctm-create-task -n "mytask" -d "This is a sample task" -c "test2001" -t "myteam"


#### Associated API: **create\_task**

Create a new Task.

Required Arguments:

* `name` - a name for the new Task.
* `team` - Team which the task belongs to.

Optional Arguments:

* `code` - a Task code.
* `desc` - a Task description.

Returns: A [Task Object](api-response-objects#task).

<h3 id="ctm-create-team" title="Permalink">ctm-create-team&nbsp;<a href="#ctm-create-team" style="display: margin-left: 1em;">&para;</a></h3>


Creates a new Team.

    REQUIRED PARAMETERS
        -n,--name                A name for the new Team.
    OPTIONAL PARAMETERS
        -d,--description         A description of the new Team
**Examples**

    ctm-create-team -n "dev"


#### Associated API: **create\_team**

Create a new team

Only an 'Administrator' can create teams.  If the credentials used for this API call
are not an Administrator, the call will not succeed.

Required Arguments:

* `name` - A name for the new Team.

Optional Arguments:

* `description` - A description of the new Team.

<h3 id="ctm-create-user" title="Permalink">ctm-create-user&nbsp;<a href="#ctm-create-user" style="display: margin-left: 1em;">&para;</a></h3>


Creates a new User, Authentication type will be set to SSO if SSO is enabled in this instance

    REQUIRED PARAMETERS
        -u,--user                A login name for the user.
        -n,--name                The full name of the user.
        -t,--teams               A list of teams the user belongs to, along
                                      with a role for each team. Teams and roles
                                      are separated by a colon. Team/role pairs
                                      are separated by commas.
        -r,--role                The users role.  (Valid values:
                                      Administrator, Developer, User)
                                      Valid Values: Administrator|Developer|User
    OPTIONAL PARAMETERS
        -p,--password            Password for the user. If "password" is
                                      not provided, a random password will be
                                      generated.
        -e,--email               Email address for the user.  Required if
                                      "password" is omitted.
        -a,--authtype            "local" or "ldap".  Default is "local" if
                                      omitted.
                                      Valid Values: local|ldap
        -f,--forcechange         Require user to change password. Default
                                      is "true" (1) if omitted. (Valid values: 0
                                      or 1).
                                      Valid Values: 0|1
        -s,--status              Status of the new account. Default is
                                      "enabled" if omitted. (Valid values:
                                      enabled, disabled, locked)
                                      Valid Values: enabled|disabled|locked
        -x,--expires             Expiration date for this account.  Must be
                                      in mm/dd/yyyy format.
        -g,--groups              A list of groups the user belongs to.
                                      Group names cannot contain spaces. Comma
                                      delimited list.
        -c,--contributors        A list of contributors the user is mapped
                                      to. Contributors cannot contain spaces.
                                      Comma delimited list.
        --get_token              Include a login token in the response.
                                      (Used for passthru login.)
**Examples**

    ctm-create-user -u "dave.thomas" -n "Dave Thomas" -r "User" -t "dev" -e "dave.thomas@example.com" -p "passw0rd" -a "local" -s "enabled"


#### Associated API: **create\_user**

Creates a new user account.

Only an 'Administrator' can create other users.  If the credentials used for this API call
are not an Administrator, the call will not succeed.

Required Arguments:

* `user` - A login name for the user.
* `name` - The full name of the user.
* `teams` - A list of teams the user belongs to, along with a role for each team. Teams and roles are separated by a
* a colon. Team/role pairs are separated by commas.

Optional Arguments:

* `password` - Password for the user. If password is not provided, a random password will be generated.
* `email` - Email address for the user.  Required if 'password' is omitted.
* `authtype` - 'local' or 'ldap'.  Default is 'local' if omitted.
* `forcechange` - Require user to change password. Default is 'true' if omitted. (Valid values: 'true' or 'false')
* `status` - Status of the new account. Default is 'enabled' if omitted. (Valid values: enabled, disabled, locked)
* `expires` - Expiration date for this account.  Default is 'never expires'. Must be in mm/dd/yyyy format.
* `groups` - A list of groups the user belongs to. Group names cannot contain spaces. Comma delimited list.
* `get_token` - If true, will return an automatic login token.  (Valid values: 1, yes, true)
* `contributors` - A list of contributors the user is mapped to. Contributors cannot contain spaces. Comma delimited list.

Returns: A [User Object](api-response-objects#user).

<h3 id="ctm-create-webhook" title="Permalink">ctm-create-webhook&nbsp;<a href="#ctm-create-webhook" style="display: margin-left: 1em;">&para;</a></h3>


Creates a new Outbound Webhook configuration.

    REQUIRED PARAMETERS
        -n,--name                The name of the Webhook
    OPTIONAL PARAMETERS
        -d,--destinationurl      URL of the REST API endpoint. ex:
                                      http://my.application.net/api/send_here
**Examples**

    ctm-create-webhook -n "MyApplication" -u "http://my.application.net/api/send_here"


#### Associated API: **create\_webhook**

Creates a new outbound Webhook configuration.

Required Arguments:

* `name` - The name of the Webhook configuration.
* `destinationurl` - The URL to which events will be posted.

Returns: Success message if successful, error message on failure.
    
<h3 id="ctm-delete-cloud-keypair" title="Permalink">ctm-delete-cloud-keypair&nbsp;<a href="#ctm-delete-cloud-keypair" style="display: margin-left: 1em;">&para;</a></h3>


Removes a key pair (ssh private key) from a Cloud endpoint definition.

    REQUIRED PARAMETERS
        -c,--cloud               The ID or Name of a Cloud.
        -n,--name                A name for the Key Pair.
**Examples**

    ctm-delete-cloud-keypair -c "us-east-1" -n "privatekey001"


#### Associated API: **delete\_cloud\_keypair**

Removes a Key Pair from a Cloud.

Required Arguments: 

* `cloud` - Name or ID of the Cloud.
* `name` - Name of the Key Pair to delete.
    
Returns: A list of [Cloud KeyPair Objects](api-response-objects#cloud-keypair).

<h3 id="ctm-delete-credential" title="Permalink">ctm-delete-credential&nbsp;<a href="#ctm-delete-credential" style="display: margin-left: 1em;">&para;</a></h3>


Deletes a Shared Credential.

    REQUIRED PARAMETERS
        -c,--credential          ID or Name of the Credential.
**Examples**

    ctm-delete-credential -c "adminuser"


#### Associated API: **delete\_credential**

Removes a Shared Credential.

Required Arguments:

* `credential` - Name or ID of the Credential to delete.

Returns: Success message if successful, error message on failure.

<h3 id="ctm-delete-package" title="Permalink">ctm-delete-package&nbsp;<a href="#ctm-delete-package" style="display: margin-left: 1em;">&para;</a></h3>


Delete a Project object.

    REQUIRED PARAMETERS
        -p,--package             Value can be either a Package ID or Name.
    OPTIONAL PARAMETERS
        --preserve               If provided, will still delete all data,
                                      but the actual Package definition will be
                                      preserved.
**Examples**

    ctm-delete-package -p "Package Name"


#### Associated API: **delete\_package**

Delete a Package Definition. Destructive of history, and there is no undo.

Required Arguments:

* `package` - the id or name of a Package.

Optional Arguments:

* `preserve` - If `true`, will delete all data but preserve the actual package definition. Valid values: true|false (default).

Returns: 'true' on success, errors on failure.

<h3 id="ctm-delete-pipeline" title="Permalink">ctm-delete-pipeline&nbsp;<a href="#ctm-delete-pipeline" style="display: margin-left: 1em;">&para;</a></h3>


Delete a Pipeline Definition.

    REQUIRED PARAMETERS
        -p,--pipeline            Value can be either a Definition ID or
                                      Name.
**Examples**

    ctm-delete-pipeline -p "PipelineName"


#### Associated API: **delete\_pipeline**

Permanently delete a Pipeline Definition.

Required Arguments:

* `pipeline` - the id or name of a Pipeline Definition.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-delete-pipelinegroup" title="Permalink">ctm-delete-pipelinegroup&nbsp;<a href="#ctm-delete-pipelinegroup" style="display: margin-left: 1em;">&para;</a></h3>


Permanently deletes a Pipeline Instance Group.

Requires the '_id' of the Pipeline Instance Group.

Returns success or failure.

    REQUIRED PARAMETERS
        -i,--pg                  ID of a Pipeline Instance Group.

#### Associated API: **delete\_pipelinegroup**

Permanently delete a Pipeline Instance Group.

> NOTE: at the moment, requires the '_id' of the Pipeline Instance Group.

Required Arguments:

* `pg` - The ID of a Pipeline Instance Group.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-delete-pipelineinstance" title="Permalink">ctm-delete-pipelineinstance&nbsp;<a href="#ctm-delete-pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>


Permanently deletes a Pipeline Instance.

Returns success or failure.

    REQUIRED PARAMETERS
        -i,--pi                  Name or ID of a Pipeline Instance.

#### Associated API: **delete\_pipelineinstance**

Permanently delete a Pipeline Instance.

Required Arguments:

* `pi` - The Name or ID of a Pipeline Instance.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-delete-plan" title="Permalink">ctm-delete-plan&nbsp;<a href="#ctm-delete-plan" style="display: margin-left: 1em;">&para;</a></h3>


Deletes a specific queued execution plan for a scheduled task.

    REQUIRED PARAMETERS
        -p,--plan_id             The integer ID of the Plan to delete.
**Examples**

    ctm-delete-plan -p 55


#### Associated API: **delete\_plan**

Deletes a specific queued execution Plan.

Required Arguments:

* `plan_id` - The integer ID of the Plan to delete.

Returns: Nothing if successful, error messages on failure.

<h3 id="ctm-delete-progression" title="Permalink">ctm-delete-progression&nbsp;<a href="#ctm-delete-progression" style="display: margin-left: 1em;">&para;</a></h3>


Delete a Progression.

    REQUIRED PARAMETERS
        -p,--progression         Value can be either a Progression ID or
                                      Name.
**Examples**

    ctm-delete-progression -p "Progression Name"


#### Associated API: **delete\_progression**

Delete a Progression Definition. Destructive of history, and there is no undo.

Required Arguments:

* `progression` - the id or name of a Progression.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-delete-project" title="Permalink">ctm-delete-project&nbsp;<a href="#ctm-delete-project" style="display: margin-left: 1em;">&para;</a></h3>


Delete a Project object.

    REQUIRED PARAMETERS
        -p,--project             Value can be either a Project ID or Name.
    OPTIONAL PARAMETERS
        --preserve               If provided, will still delete all data,
                                      but the actual Project will be preserved.
**Examples**

    ctm-delete-project -p "ProjectName"


#### Associated API: **delete\_project**

Permanently delete a Project.

Required Arguments:

* `project` - the id or name of a Project.

Optional Arguments:

* `preserve` - If `true`, will delete all data but preserve the actual project. Valid values: true|false (default).

Returns: 'true' on success, errors on failure.

<h3 id="ctm-delete-task" title="Permalink">ctm-delete-task&nbsp;<a href="#ctm-delete-task" style="display: margin-left: 1em;">&para;</a></h3>


Deletes a Task.

    REQUIRED PARAMETERS
        -t,--task                The ID or Name of the Task to delete.
    OPTIONAL PARAMETERS
        -f,--force_delete        Force the deletion of a Task, even if it
                                      has history and references.
**Examples**

_To delete a task that does not have any runtime history_

    ctm-delete-task -t "mytask01"

_To force a delete of a task that has runtime history_

    ctm-delete-task -f "mytask01" -f


#### Associated API: **delete\_task**

Deletes all versions of a Task.

Required Arguments:

* `task` - Either the Task ID or Name.

Optional Arguments:

* `force_delete` - Delete the Task, even if there are historical rows and references.  (Valid values: 1, yes, true)

Returns: Nothing if successful, error messages on failure.

<h3 id="ctm-delete-user" title="Permalink">ctm-delete-user&nbsp;<a href="#ctm-delete-user" style="display: margin-left: 1em;">&para;</a></h3>


Deletes a new User.

    REQUIRED PARAMETERS
        -u,--user                A login name for the user.
**Examples**

    ctm-delete-user -u "dave.thomas"


#### Associated API: **delete\_user**

Deletes a user account
Only an 'Administrator' can manage other users.  If the credentials used for this API call
are not an Administrator, the call will not succeed.

Properties will only be updated if the option is provided.  Omitted properties will not be changed.

NOTE: the "username" of a user cannot be changed.

If a user has 'locked' their account by numerous failed login attempts, the flag is reset
by setting any property.  It's easiest to just the status to 'enabled'.

Required Arguments:

* `user` - ID or Name of the User to update.

        
<h3 id="ctm-deliver-packagerevision" title="Permalink">ctm-deliver-packagerevision&nbsp;<a href="#ctm-deliver-packagerevision" style="display: margin-left: 1em;">&para;</a></h3>


`Delivers` a Package Revision out of a Progression into a Delivered condition.

    REQUIRED PARAMETERS
        -p,--package             Name of the Package to promote to a
                                      Progression Phase.
    OPTIONAL PARAMETERS
        -r,--revision            Revision number of a Package to promote,
                                      takes precedence over "full_version".
        -f,--full_version        Optional Full Version of package to
                                      promote, optional alternative selector to
                                      "revision".
**Examples**

    ctm-deliver-packagerevision -p "Some Package Name" -r 205

    - or -

    ctm-deliver-revision -p "Some Package Name" -f "15.2.3.205"


#### Associated API: **deliver\_revision**

Delivers a Package Revision out of a Progression into a Delivered condition.

Required Arguments:

* `package` - Name of the Package.
* `revision` - Revision number of a Package to deliver, takes precedence over `full_version`.
* `full_version` - Optional Full Version of package to deliver, optional alternative selector to `revision`.

Returns: `success` on success, errors otherwise.

<h3 id="ctm-describe-api" title="Permalink">ctm-describe-api&nbsp;<a href="#ctm-describe-api" style="display: margin-left: 1em;">&para;</a></h3>


Retrieves a list of all REST API methods and their documentation.

    OPTIONAL PARAMETERS
        -l,--listonly            List the methods without documentation.
**Examples**

_To print a full listing of all api commands with documentation_

    ctm-describe-api

_To print only the names with the api commands sorted_

    ctm-describe-api -l


<h3 id="ctm-export-canvas" title="Permalink">ctm-export-canvas&nbsp;<a href="#ctm-export-canvas" style="display: margin-left: 1em;">&para;</a></h3>


Exports Canvas items to a directory.

    OPTIONAL PARAMETERS
        -p,--project             If provided, limits export to a specific
                                      Project.
        -c,--component           If provided, limits a Project to a
                                      specific Component. (project is required.)
        -r,--repository          Specify either "file" or "db" repository.
                                      ("db" if omitted.)
        -o,--outputdirectory     Directory where the output will be saved.
                                      The directory must exist, and should be
                                      empty.
        --printoutput            If provided, no file will be created.  The
                                      results of the API call will be printed.

#### Associated API: **export\_canvas**

Generates an export JSON document all Canvas items.

This function is capable of exporting items from the "filesystem" repository, which is an administrative feature.

Optional Arguments:

* `project` - filter by a Canvas Project name.
* `component` - filter by a Canvas Component. (Project is required.)
* `repository` - specify the repository ('file' or 'db', 'db' if omitted.)

Returns: A JSON document containing Canvas items.

<h3 id="ctm-export-catalog" title="Permalink">ctm-export-catalog&nbsp;<a href="#ctm-export-catalog" style="display: margin-left: 1em;">&para;</a></h3>


Export all Project, Pipeline, Package, and Task definitions to a catalog as JSON documents.

    OPTIONAL PARAMETERS
        -o,--outputdirectory     Directory where the output will be saved.
                                      The directory must exist, and should be
                                      empty.
        -t,--team                Team "name" or id, To export the assets of
                                      specified team.
                                      Multiple teams can be specified using
                                      comma. E.g. "Dev Team","Test Team"
**Examples**

_To export a catalog of backup files._

    ctm-export-catalog -o myoutputdirectory -t "teamname or teamid"


#### Associated API: **export\_catalog**

Export all Project, Pipeline, Package, and Task definitions to a catalog as a JSON document.

Returns: A JSON document containing all Project, Pipeline, Package, and Task definitions.

<h3 id="ctm-export-package" title="Permalink">ctm-export-package&nbsp;<a href="#ctm-export-package" style="display: margin-left: 1em;">&para;</a></h3>


Export a Package Definition as a portable backup JSON document.

    REQUIRED PARAMETERS
        -p,--package             Value can be either a Package Definition
                                      ID or Name.
**Examples**

    ctm-export-package -p "Some Package Name"


#### Associated API: **export\_package**

Export a Package Definition as a portable backup JSON document.

Required Arguments:

* `package` - the id or name of a Package.

Returns: A [Package Definition Object](api-response-objects#package-definition).

<h3 id="ctm-export-pipeline" title="Permalink">ctm-export-pipeline&nbsp;<a href="#ctm-export-pipeline" style="display: margin-left: 1em;">&para;</a></h3>


Exports a Pipeline Definition backup file.  Includes complete versions of all Phases and Stages.

    REQUIRED PARAMETERS
        -p,--pipeline            Value can be either a Definition ID or
                                      Name.
**Examples**

_To export a Pipeline backup file._

    ctm-export-pipeline -p "MyPipeline" > mypipeline.json 


#### Associated API: **export\_pipeline**

Export a Pipeline Definition as a portable backup JSON document.

Required Arguments:

* `pipeline` - the id or name of a Pipeline Definition.

Returns: A [Pipeline Definition Object](api-response-objects#pipeline-definition).

<h3 id="ctm-export-plugins" title="Permalink">ctm-export-plugins&nbsp;<a href="#ctm-export-plugins" style="display: margin-left: 1em;">&para;</a></h3>


Export Plugin configurations as a portable backup JSON document.

    OPTIONAL PARAMETERS
        -n,--name                Optional name to export only a specified
                                      Plugin.
**Examples**

    ctm-export-plugin -n "Specific Plugin Name"


#### Associated API: **export\_plugins**


<h3 id="ctm-export-progression" title="Permalink">ctm-export-progression&nbsp;<a href="#ctm-export-progression" style="display: margin-left: 1em;">&para;</a></h3>


Export a Progression Definition as a portable backup JSON document.

    REQUIRED PARAMETERS
        -p,--progression         Value can be either a Progression
                                      Definition ID or Name.
**Examples**

    ctm-export-progression -p "Some Progression Name"


#### Associated API: **export\_progression**

Export a Progression Definition as a portable backup JSON document.

Required Arguments:

* `progression` - the id or name of a Progression.

Returns: A [Progression Definition Object](api-response-objects#progression-definition).

<h3 id="ctm-export-project" title="Permalink">ctm-export-project&nbsp;<a href="#ctm-export-project" style="display: margin-left: 1em;">&para;</a></h3>


Gets a Project Definition for export.

    REQUIRED PARAMETERS
        -p,--project             Value can be either a Project ID or Name.
**Examples**

    ctm-export-project -p "ProjectName" > myproject.json


#### Associated API: **export\_project**

Gets a Project object for export.  (Will not include the `_id`.)

Required Arguments:

* `project` - the id or name of a Project.

Returns: A [Project Object](api-response-objects#project).

<h3 id="ctm-export-task" title="Permalink">ctm-export-task&nbsp;<a href="#ctm-export-task" style="display: margin-left: 1em;">&para;</a></h3>


Exports a Task that can be checked into version control or imported elsewhere.

    REQUIRED PARAMETERS
        -t,--task                The ID or Name of the Task to export.
    OPTIONAL PARAMETERS
        -r,--include_refs        If provided, will include all referenced
                                      subtasks.
        -f,--output_file         Save the exported Task(s) to the specified
                                      file.
**Examples**

_To export the default version of a task in the default xml format_

    ctm-export-task -t "mytask01"

_To export the of a task, include all subtask references and put results in a file_

    ctm-export-task -t "mytask01" -r -f "~/mytask01.xml"


#### Associated API: **export\_task**

Create a backup file for a single Task.

> The behavior of this command is different depending on the `Accept` header.

* If 'application/json' (default), it will return a JSON list of individual Task documents.
* If 'application/xml' OR 'text/plain', it will return an XML document of Tasks.

Required Arguments:

* `task` - Value can be either a Task ID, Code or Name.

Optional Arguments:

* `include_refs`` - If true, will analyze each task and include any referenced Tasks.

Returns: A collection of Task backup objects.

<h3 id="ctm-get-active-tasks" title="Permalink">ctm-get-active-tasks&nbsp;<a href="#ctm-get-active-tasks" style="display: margin-left: 1em;">&para;</a></h3>


Gets a list of active Task Instances (Submitted, Staged, Pending, Processing).

    OPTIONAL PARAMETERS
        -f,--filter              A filter.
        -r,--records             Maximum number of records to return.
**Examples**

_Get all active task instances_

    ctm-get-active-tasks

_Get all active task instances that have a status of Processing_

    ctm-get-active-tasks -f "Processing"

_Get all active task instance with a particular string in the name_

    ctm-get-active-tasks -f "mytask01"

_Limit the number of task instances returned_

    ctm-get-active-tasks -r 10


#### Associated API: **get\_task\_instances**

Gets a list of Task Instances.

Optional Arguments:

* `filter` - A filter to limit the results.
* `status` - A comma separated list of statuses to filter the results.
* `from` - a date string to set as the "from" marker. (mm/dd/yyyy format)
* `to` - a date string to set as the "to" marker. (mm/dd/yyyy format)
* `records` - a maximum number of results to get.

Returns: A list of [Task Instance Objects](api-response-objects#task-instance).

<h3 id="ctm-get-asset" title="Permalink">ctm-get-asset&nbsp;<a href="#ctm-get-asset" style="display: margin-left: 1em;">&para;</a></h3>


Prints the properties of an Asset

    REQUIRED PARAMETERS
        -a,--asset               The ID or Name of an Asset.
**Examples**

    ctm-get-asset -a "database001"


#### Associated API: **get\_asset**

Gets an Asset.

Required Arguments:

* `asset` - an Asset Name or ID.

Returns: An [Asset Object](api-response-objects#asset).

<h3 id="ctm-get-cloud" title="Permalink">ctm-get-cloud&nbsp;<a href="#ctm-get-cloud" style="display: margin-left: 1em;">&para;</a></h3>


Prints the properties of a Cloud endpoint

    REQUIRED PARAMETERS
        -n,--name                The ID or Name of a Cloud.
**Examples**

    ctm-get-cloud -n "us-east-1"


#### Associated API: **get\_cloud**

Gets a Cloud object.

Required Arguments: 

* `name` - a Cloud name or ID.

Returns: A [Cloud Object](api-response-objects#cloud).

<h3 id="ctm-get-license" title="Permalink">ctm-get-license&nbsp;<a href="#ctm-get-license" style="display: margin-left: 1em;">&para;</a></h3>


Prints the license information including expiration date

**Examples**

    ctm-get-license


#### Associated API: **get\_license**

Get the license details.

Required Arguments:

* `license` - The text of a license key provided by Continuum.

Returns: The relevant properties of the current license.

<h3 id="ctm-get-next-id" title="Permalink">ctm-get-next-id&nbsp;<a href="#ctm-get-next-id" style="display: margin-left: 1em;">&para;</a></h3>


Get the next ID in an ID set

    REQUIRED PARAMETERS
        -n,--name                ID set name
    OPTIONAL PARAMETERS
        -r,--reseed              Reseed the ID set starting with this
                                      number
        -f,--fallback            Fallback to this number if there is an
                                      exception

#### Associated API: **get\_next\_id**

Get the next integer `id` in a named ID set.

Required Arguments:

* `name` - the name of the ID set

Optional Arguments:

* `reseed` - (integer) If provided, reset the pool to the specified value.  (This is the value that will be returned.)
* `fallback` - (integer) In the case of any errors, the provided `fallback` number will be returned. `0` if omitted.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-get-package" title="Permalink">ctm-get-package&nbsp;<a href="#ctm-get-package" style="display: margin-left: 1em;">&para;</a></h3>


Get the definition document of a Package.

    REQUIRED PARAMETERS
        -p,--package             Value can be either a Package Definition
                                      ID or Name.
**Examples**

    ctm-get-get_package-manifest -p "Some Package Name"


#### Associated API: **get\_package**

Returns the definition of the specified Package.

Required Arguments:

* `package` - Name of the Package.

Returns: The Package definition document.

<h3 id="ctm-get-package-manifest" title="Permalink">ctm-get-package-manifest&nbsp;<a href="#ctm-get-package-manifest" style="display: margin-left: 1em;">&para;</a></h3>


Get the Manifest of a Package, for the specified version and range of revisions.

    REQUIRED PARAMETERS
        -p,--package             Value can be either a Package Definition
                                      ID or Name.
    OPTIONAL PARAMETERS
        -v,--version             Optional Package Version. (All Versions if
                                      omitted.)
        -f,--from                From Revision. (First (oldest) Revision in
                                      the range if omitted.)
        -t,--to                  To Revision. (Last (newest) Revision in
                                      the range if omitted.)
        -t,--to                  To Revision. (Last (newest) Revision in
                                      the range if omitted.)
        --verbose                Verbose data for result objects.
**Examples**

    ctm-get-package-manifest -p "Some Package Name" -v "Specific Version" -f "From Revision" -t "To Revision"


#### Associated API: **get\_package\_manifest**

Returns the complete Manifest of a Package Version, given a range of Revisions.

Required Arguments:

* `package` - Name of the Package.

Optional Arguments:

* `version` - Version of the Package.  If omitted, optionally use...
* `version_of_rev` - (integer) A specific Revision. If provided, discover and use the Version of this specific Revision.

> Note: If both `version` and `version_of_rev` are provided, `version` takes precedence.

* `from` - (integer) A starting (older) Revision.  If omitted, will use the oldest Revision in the specified Version.
* `to` - (integer) An ending (later) Revision.  If omitted, will use the newest Revision in the specified Version.
* `verbose` - (`true`/`false`) Return verbose Manifest details.  `false` if omitted.

Returns: The Manifest (Workitems, Changes and Artifacts) contained in the specified Package Revision range.

<h3 id="ctm-get-piartifacts" title="Permalink">ctm-get-piartifacts&nbsp;<a href="#ctm-get-piartifacts" style="display: margin-left: 1em;">&para;</a></h3>


Gets the Artifacts from the Manifest of a Pipeline Instance.

    REQUIRED PARAMETERS
        -i,--pi                  Value can be either a Pipeline Instance ID
                                      or Name.
**Examples**

    ctm-get-piartifacts -i "Pipeline Instance Name or ID"


#### Associated API: **get\_pi\_artifacts**

Gets the Changes from the Manifest of a Pipeline Instance.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Returns: A JSON document representing all Changes on the Manifest.

> Note: the response is 'json' - 'text' and 'xml' object_output options are not supported.

<h3 id="ctm-get-pichanges" title="Permalink">ctm-get-pichanges&nbsp;<a href="#ctm-get-pichanges" style="display: margin-left: 1em;">&para;</a></h3>


Gets the Changes from the Manifest of a Pipeline Instance.

    REQUIRED PARAMETERS
        -i,--pi                  Value can be either a Pipeline Instance ID
                                      or Name.
**Examples**

    ctm-get-pichanges -i "Pipeline Instance Name or ID"


#### Associated API: **get\_pi\_changes**

Gets the Changes from the Manifest of a Pipeline Instance.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Returns: A JSON document representing all Changes on the Manifest.

Note: the response is 'json' - 'text' and 'xml' object_output options are not supported.

<h3 id="ctm-get-pidata" title="Permalink">ctm-get-pidata&nbsp;<a href="#ctm-get-pidata" style="display: margin-left: 1em;">&para;</a></h3>


Gets a Pipeline Instance Data object.

    REQUIRED PARAMETERS
        -i,--pi                  Value can be either a Pipeline Instance ID
                                      or Name.
    OPTIONAL PARAMETERS
        -l,--lookup              Lookup an expression that evaluates to a
                                      subsection of the document.
**Examples**

    ctm-get-pidata -i "Pipeline Instance Name or ID"


#### Associated API: **get\_pi\_data**

Gets a Pipeline Instance Data object.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Optional Arguments:

* `lookup` - Lookup using an expression that evaluates to a subsection of the document.

Returns: A [Pipeline Instance](api-response-objects#pipeline-instance).

Note: the response is 'json' - 'text' and 'xml' object_output options are not supported.

<h3 id="ctm-get-pipeline" title="Permalink">ctm-get-pipeline&nbsp;<a href="#ctm-get-pipeline" style="display: margin-left: 1em;">&para;</a></h3>


Gets a Pipeline Definition.

    REQUIRED PARAMETERS
        -p,--pipeline            Value can be either a Definition ID or
                                      Name.
**Examples**

    ctm-get-pipeline -p "PipelineName"


#### Associated API: **get\_pipeline**

Gets a Pipeline Definition object.

Required Arguments:

* `pipeline` - the id or name of a Pipeline Definition.

Returns: A [Pipeline Definition Object](api-response-objects#pipeline-definition).

<h3 id="ctm-get-pipelineinstance" title="Permalink">ctm-get-pipelineinstance&nbsp;<a href="#ctm-get-pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>


Gets a Pipeline Instance object.

    REQUIRED PARAMETERS
        -i,--pi                  Value can be either a Pipeline Instance ID
                                      or Name.
    OPTIONAL PARAMETERS
        -s,--include_stages      If provided, include the Stages, Steps and
                                      Plugins - the whole enchilada.
**Examples**

    ctm-get-pipelineinstance -i "Pipeline Instance Name or ID"


#### Associated API: **get\_pipelineinstance**

Gets a Pipeline Instance object.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Optional Arguments:

* `include_stages` - include Stage, Step and Plugin data and status.

Returns: A [Pipeline Instance](api-response-objects#pipeline-instance).

<h3 id="ctm-get-piworkitems" title="Permalink">ctm-get-piworkitems&nbsp;<a href="#ctm-get-piworkitems" style="display: margin-left: 1em;">&para;</a></h3>


Gets the Workitems from the Manifest of a Pipeline Instance.

    REQUIRED PARAMETERS
        -i,--pi                  Value can be either a Pipeline Instance ID
                                      or Name.
**Examples**

    ctm-get-piworkitems -i "Pipeline Instance Name or ID"


#### Associated API: **get\_pi\_workitems**

Gets the Workitems from the Manifest of a Pipeline Instance.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Returns: A JSON document representing all Workitems on the Manifest.

Note: the response is 'json' - 'text' and 'xml' object_output options are not supported.

<h3 id="ctm-get-project" title="Permalink">ctm-get-project&nbsp;<a href="#ctm-get-project" style="display: margin-left: 1em;">&para;</a></h3>


Gets a Project Definition.

    REQUIRED PARAMETERS
        -p,--project             Value can be either a Project ID or Name.
**Examples**

    ctm-get-project -p "ProjectName"


#### Associated API: **get\_project**

Gets a Project object.

Required Arguments:

* `project` - the id or name of a Project.

Returns: A [Project Object](api-response-objects#project).

<h3 id="ctm-get-settings" title="Permalink">ctm-get-settings&nbsp;<a href="#ctm-get-settings" style="display: margin-left: 1em;">&para;</a></h3>


Gets all the configuration settings from the database in json format

    OPTIONAL PARAMETERS
        -m,--module              Filter to a specific module.
**Examples**

_To get all config settings in text format_

    ctm-get-settings

_To get all config settings in json format_

    ctm-get-settings -F "json"

_To get the settings only for the messenger module_

    ctm-get-settings -m "Messenger"

_To get a list of the module names available in the settings configurations_
   
    ctm-get-settings |grep -v "^ "|grep -v "^$"


#### Associated API: **get\_settings**

Lists all the settings of modules.

Optional Arguments:

* `module` - name of the module. If omitted, all module settings are returned.

Returns: A [Settings Object](api-response-objects#settings).

<h3 id="ctm-get-submission" title="Permalink">ctm-get-submission&nbsp;<a href="#ctm-get-submission" style="display: margin-left: 1em;">&para;</a></h3>


Gets the raw payload of a specific 'Submission' via a MongoDB query.

For query syntax, see the MongDB find() syntax:
http://docs.mongodb.org/manual/reference/method/db.collection.find

Returns the submission document, or a 'not found' message.

    REQUIRED PARAMETERS
        -q,--query               A query in JSON format.
**Examples**

_To find a Submission using the 'after' property:_

    ctm-get-submission -q '{"after" : "abc123"}'


#### Associated API: **get\_submission**

Gets a raw 'Submission' payload using a query.

Required Arguments:

* `query` - Valid MongoDB query to identify the previous payload to resubmit.

> If the query would return multiple submissions, the newest one is matched.

Returns: the Submission document on success, 'not found' otherwise.

<h3 id="ctm-get-system-log" title="Permalink">ctm-get-system-log&nbsp;<a href="#ctm-get-system-log" style="display: margin-left: 1em;">&para;</a></h3>


Get the System Log.

    OPTIONAL PARAMETERS
        -i,--object_id           An Object ID filter.
        -t,--object_type         The integer representation of an internal
                                      object type. Can be used with one of the
                                      following when log_type = Object: (User =
                                      1, Asset = 2, Task = 3, Schedule = 4, Tag
                                      = 7, Image = 8, MessageTemplate = 18,
                                      Parameter = 34, Credential = 35, Domain =
                                      36, CloudAccount = 40, Cloud = 41,
                                      CloudKeyPair = 45)
        -u,--user                A user name to filter result on.
        -l,--log_type            The type of log, either Object or Security
        -a,--action              The action that triggered a log entry. One
                                      of the following: (UserLogin, UserLogout,
                                      UserLoginAttempt, UserPasswordChange,
                                      UserSessionDrop, ObjectAdd, ObjectModify,
                                      ObjectDelete, bjectView, ObjectCopy,
                                      ConfigChange)
        -f,--filter              A filter whereby the results would contain
                                      this string
        --from                   A "from" date in the format of m/d/yyyy.
        --to                     A "to" date in the format of m/d/yyyy.
        -r,--records             Maximum number of records to return,
                                      default is 100.
**Examples**

_To get the last 100 denied login attempts_

    ctm-get-system-log -l "Security" -a "UserLoginAttempt"

_To get any log entries attributed to the administrator user between two dates_

    ctm-get-system-log -u "administrator" -l "Object" --from "1/6/2014" --to "1/7/2014"

_To get the last 300 task modifications_

    ctm-get-system-log -t 3 -r 300


#### Associated API: **get\_system\_log**

Gets the system log.  If all arguments are omitted, will return the most recent 100 entries.

Optional Arguments:

* `object_id` - An object_id filter to limit the results.
* `object_type` - An object_type filter to limit the results.
* `log_type` - A log_type filter. ('Security' or 'Object')
* `action` - An action filter.
* `filter` - A filter to limit the results.
* `from` - a date string to set as the "from" marker. (mm/dd/yyyy format)
* `to` - a date string to set as the "to" marker. (mm/dd/yyyy format)
* `records` - a maximum number of results to get.

Returns: A list of [Log Entry Objects](api-response-objects#log-entry).

<h3 id="ctm-get-task" title="Permalink">ctm-get-task&nbsp;<a href="#ctm-get-task" style="display: margin-left: 1em;">&para;</a></h3>


Prints the properties of a Task

    REQUIRED PARAMETERS
        -t,--task                The ID or Name of a Task.
    OPTIONAL PARAMETERS
        -i,--include_code        Include all task step code, if
                                      output_format is "json" or "xml".
**Examples**

_To print the high level properties of a specific Task

    ctm-get-task -t "mytask01"

_To print the properties and code of the default version of a Task_

    ctm-get-task -t "new example" -i


#### Associated API: **get\_task**

Gets a Task object.

Required Arguments:

* `task` - Value can be either a Task ID or Name.

Optional Arguments:

* `include_code` - Whether to include Codeblocks and Steps.  (Only included if 'output_format' is 'json' or 'xml'.  'False' if omitted.)

Returns: A [Task Object](api-response-objects#task).

<h3 id="ctm-get-task-instance" title="Permalink">ctm-get-task-instance&nbsp;<a href="#ctm-get-task-instance" style="display: margin-left: 1em;">&para;</a></h3>


Get the properties of a Task Instance such as status, submitted and completed dates, etc.

    REQUIRED PARAMETERS
        -i,--instance            The Task Instance number.
**Examples**

    ctm-get-task-instance -i 43669


#### Associated API: **get\_task\_instance**

Gets the details of a Task Instance.

Required Arguments:
* `instance` - The Task Instance identifier.

Returns: A [Task Instance Object](api-response-objects#task-instance).

<h3 id="ctm-get-task-instances" title="Permalink">ctm-get-task-instances&nbsp;<a href="#ctm-get-task-instances" style="display: margin-left: 1em;">&para;</a></h3>


Get a list of Task Instances and their properties (status, dates, etc.).

    OPTIONAL PARAMETERS
        -f,--filter              A filter.
        -s,--status              A comma separated list of statuses.
        --from                   A "from" date.
        --to                     A "to" date.
        -r,--records             Maximum number of records to return.
**Examples**

_To retrieve the the last 200 task instances_

    ctm-get-task-instances

_To get all Processing and Submitted task instances, max 200_

    ctm-get-task-instances -s "Processing,Submitted"

_To get a set of task instances between two dates_

    ctm-get-task-instances --from "01/14/2014" --to "01/16/2014"

_To get the last 1000 task instances, overriding the default max of 200_

    ctm-get-task-instances -r 1000

_To get the last 10 task instance for any tasks with a particular string in the name_

    ctm-get-task-instances -r 10 -f "mytask01"


#### Associated API: **get\_task\_instances**

Gets a list of Task Instances.

Optional Arguments:

* `filter` - A filter to limit the results.
* `status` - A comma separated list of statuses to filter the results.
* `from` - a date string to set as the "from" marker. (mm/dd/yyyy format)
* `to` - a date string to set as the "to" marker. (mm/dd/yyyy format)
* `records` - a maximum number of results to get.

Returns: A list of [Task Instance Objects](api-response-objects#task-instance).

<h3 id="ctm-get-task-plans" title="Permalink">ctm-get-task-plans&nbsp;<a href="#ctm-get-task-plans" style="display: margin-left: 1em;">&para;</a></h3>


Gets a list of queued schedule execution plans for a task.

    REQUIRED PARAMETERS
        -t,--task                The ID or Name of a Task.
**Examples**

_Get all scheduled execution plans for a particular task_

    ctm-get-task-plans -t "mytask01"


#### Associated API: **get\_task\_plans**

Gets a list of the queued execution plans for a Task.

Required Arguments:

* `task` - Value can be either a Task ID or Name.

Optional Arguments:

Returns: A list of [Execution Plan Objects](api-response-objects#execution-plan).

<h3 id="ctm-get-task-schedules" title="Permalink">ctm-get-task-schedules&nbsp;<a href="#ctm-get-task-schedules" style="display: margin-left: 1em;">&para;</a></h3>


Gets a list of schedule definitions for a given task.

    REQUIRED PARAMETERS
        -t,--task                The ID or Name of a Task.
**Examples**

_To list the schedules for a particular task_

    ctm-get-task-schedules -t "mytask01"


#### Associated API: **get\_task\_schedules**

Gets a list of Schedule definitions for a Task.

Required Arguments:

* `task` - Value can be either a Task ID or Name.

Optional Arguments:

Returns: A list of [Task Schedule Objects](api-response-objects#task-schedule).

* Text results do not include timing details.
* JSON results include Schedule definitions suitable for use in the 'schedule_task' function.

<h3 id="ctm-get-worklist" title="Permalink">ctm-get-worklist&nbsp;<a href="#ctm-get-worklist" style="display: margin-left: 1em;">&para;</a></h3>


Gets a list of pending Pipeline Instances.

    OPTIONAL PARAMETERS
        -f,--filter              Limit the result to a specific key:value
                                      pair.
**Examples**

    ctm-get-worklist -f "key:value"


#### Associated API: **get\_worklist**

Gets a list of Pipeline in 'pending' status.

Optional Arguments:

* `filter` - a key:value filter to limit the results.

Returns: A list of pending Pipeline Instances.

<h3 id="ctm-import-backup" title="Permalink">ctm-import-backup&nbsp;<a href="#ctm-import-backup" style="display: margin-left: 1em;">&para;</a></h3>


DEPRECATED: Please use `ctm-import-task`.
    
    Imports a task backup file into the system. This file can include one or
                    more tasks within it and must be XML or JSON formatted

    REQUIRED PARAMETERS
        -f,--file                The file name of the backup file.
    OPTIONAL PARAMETERS
        -c,--on_conflict         Action to take if one or more Tasks have a
                                      conflict. "replace", "cancel".
**Examples**

    ctm-import-backup -f ~/mytask01.xml


#### Associated API: **import\_backup**

Imports an XML or JSON backup file.

> DEPRECATED: this function is deprecated.  Use `import_task` instead.

Required Arguments:

* `import_text` - An XML or JSON document in the format of a Task backup file.

Returns: A list of items in the backup file, with the success/failure of each import.

<h3 id="ctm-import-canvas" title="Permalink">ctm-import-canvas&nbsp;<a href="#ctm-import-canvas" style="display: margin-left: 1em;">&para;</a></h3>


Imports Canvas items from a properly formatted directory.

    OPTIONAL PARAMETERS
        -i,--inputdirectory      Directory where the Canvas files exist.
                                      Current directory if omitted.
        -r,--repository          "Specify either "file" or "db" repository.
                                      "db" if omitted.
                                      Only Administrators are allowed to use the
                                      "file" option.
        --ignoreconflicts        If provided, the import process will
                                      handle Name conflicts aggressively. If
                                      Canvas items with the same
                                      Project/Component/Name exist, they will be
                                      overwritten.

#### Associated API: **create\_canvas\_item**

Creates a new Canvas item.

Required Arguments:

* `project` - a Canvas Project name.
* `component` - a Canvas Component name.
* `name` - a Canvas item name.
* `resourcedata` - the content of the item.

Optional Arguments:

* `ignoreconflicts` - if 'true' existing items will be overwritten.

Returns: Success or Error message.

<h3 id="ctm-import-catalog" title="Permalink">ctm-import-catalog&nbsp;<a href="#ctm-import-catalog" style="display: margin-left: 1em;">&para;</a></h3>


Import all Project, Pipeline, Package, and Task definitions from a catalog as JSON documents.

    OPTIONAL PARAMETERS
        -i,--inputdirectory      Directory where the input files are
                                      located.  The directory must exist.
        -t,--team                Team "name" or id, To import the assets in
                                      specified team.
                                      Multiple teams can be specified using
                                      comma. E.g. "Dev Team","Test Team"
        -o,--overwrite           Valid values: true|false (default).
**Examples**

_To import a catalog from backup files._

    ctm-import-catalog -i myinputdirectory -t "teamname or teamid"


#### Associated API: **import\_catalog**

Import all Project, Pipeline, Package, and Task definitions from a catalog as a JSON document.

Optional Arguments:

* `projects` - An array of project JSON objects to import.
* `pipelines` - An array of pipeline JSON objects to import.
* `packages` - An array of package JSON objects to import.
* `tasks` - An array of task JSON objects to import.
* `overwrite` - Valid values: true|false (default).
    If 'overwrite' is 'true' and the Definition exists, it will be replaced.
* `human_readable` -  Valid values: true (default)|false.
    Whether to provide output as name/messgae or id/(true or false).
    It might be useful to set this to false if you are importing the catalog as part of some automation.
* `import_into_team` - Team "name" or id. If specified, the catalog will be imported into the specified team, rather than the teams specified in the input.
                                This may be useful if you wish to import items from another team or Continuum instance

Returns: A list of all Project, Pipeline, Package, and Task definitions with the name and status of import or exception.

<h3 id="ctm-import-package" title="Permalink">ctm-import-package&nbsp;<a href="#ctm-import-package" style="display: margin-left: 1em;">&para;</a></h3>


Imports a backup of a Package Definition..

Returns success or error.

    REQUIRED PARAMETERS
        -b,--backupfile          A JSON document formatted as a Package
                                      backup.
    OPTIONAL PARAMETERS
        -o,--overwrite           Valid values: true|false (default).

#### Associated API: **import\_package**

Import a Package Definition from a backup file.

Required Arguments:

* `backup` - A JSON document formatted as a Package Definition backup.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

> If 'overwrite' is 'true' and the Definition exists, it will be replaced.

Returns: Success or error.

<h3 id="ctm-import-pipeline" title="Permalink">ctm-import-pipeline&nbsp;<a href="#ctm-import-pipeline" style="display: margin-left: 1em;">&para;</a></h3>


Imports a Pipeline Definition from a JSON document.

Returns a Pipeline Object.

    REQUIRED PARAMETERS
        -b,--backupfile          A JSON document formatted as a complete
                                      Pipeline Definition backup.
    OPTIONAL PARAMETERS
        -o,--overwrite           Valid values: pipeline|phases|all|none
                                      (default).

#### Associated API: **import\_pipeline**

Import a Pipeline Definition.

Required Arguments:

* `backup` - A JSON document formatted as a complete Continuum Pipeline Definition backup.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

    If 'overwrite' is 'true' and the Definition exists, it will be replaced.

Returns: A [Pipeline Definition Object](api-response-objects#pipeline-definition).

<h3 id="ctm-import-progression" title="Permalink">ctm-import-progression&nbsp;<a href="#ctm-import-progression" style="display: margin-left: 1em;">&para;</a></h3>


Imports a backup of a Progression Definition..

Returns success or error.

    REQUIRED PARAMETERS
        -b,--backupfile          A JSON document formatted as a Progression
                                      backup.
    OPTIONAL PARAMETERS
        -o,--overwrite           Valid values: true|false (default).

#### Associated API: **import\_progression**

Import a Progression Definition from a backup file.

Required Arguments:

* `backup` - A JSON document formatted as a Progression Definition backup.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

    If 'overwrite' is 'true' and the Progression exists, it will be replaced.

Returns: Success or error.

<h3 id="ctm-import-project" title="Permalink">ctm-import-project&nbsp;<a href="#ctm-import-project" style="display: margin-left: 1em;">&para;</a></h3>


Imports a Project Definition from a JSON document.

Returns a Project Object.

    REQUIRED PARAMETERS
        -b,--backupfile          A JSON document formatted as a complete
                                      Project backup.
    OPTIONAL PARAMETERS
        -o,--overwrite           Valid values: true|false (default).

#### Associated API: **import\_project**

Import a Project.

Required Arguments:

* `backup` - A JSON document formatted as a complete Project backup.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

    If 'overwrite' is 'true' the Project will be replaced.

Returns: A [Project Object](api-response-objects#project).

<h3 id="ctm-import-task" title="Permalink">ctm-import-task&nbsp;<a href="#ctm-import-task" style="display: margin-left: 1em;">&para;</a></h3>


Imports a Task backup file. This file can include one or
                    more tasks within it and must be JSON formatted.

    REQUIRED PARAMETERS
        -f,--file                The file name of the backup file.
    OPTIONAL PARAMETERS
        -c,--on_conflict         Action to take if one or more Tasks have a
                                      conflict. "replace", "cancel".
**Examples**

    ctm-import-backup -f ~/mytask02.json


#### Associated API: **import\_task**

Imports a Task backup file.

Required Arguments:

* `backup` - A JSON document in the format of a Task backup file.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

    If 'overwrite' is 'true' the Task(s) will be replaced.

> NOTE: There may be multiple Tasks in a single backup file, as often Tasks have dependencies on other Tasks, so all are included.

Returns: A list of items in the backup file, with the success/failure of each import.

<h3 id="ctm-initiate-pipeline" title="Permalink">ctm-initiate-pipeline&nbsp;<a href="#ctm-initiate-pipeline" style="display: margin-left: 1em;">&para;</a></h3>


Initiate a Pipeline Definition with matching 'key' information.

Returns a Pipeline Instance Object.

    REQUIRED PARAMETERS
        -d,--definition          Pipeline Definition to initiate.
        -p,--project             The Project name with which to associate
                                      this instance.
        -g,--group               Descriptive label of a group to summarize
                                      multiple instances of this
                                      definition/project.
    OPTIONAL PARAMETERS
        -n,--name                An explicit name for the unique instance.
                                      (Autogenerated if omitted.)
        -j,--details             A JSON object with additional details
                                      about this instance.

#### Associated API: **initiate\_pipeline**

Attempt to initiate a Pipeline Definition.

Required Arguments:

* `definition` - ID or Name of a Pipeline Definition to initiate.
* `project` - An identifying name for a Project. (ie: repo name)  Useful if a single pipeline definition supports multiple projects.
* `group` - Summary name, (ie: branch name) used to group all runs of this definition/project combination. Describes your 'use' of this Pipeline.

Optional Arguments:

* `instance_name` - An explicit name to use for this unique run.  (ie: commit id)
* `details` - a JSON object with additional properties for the Pipeline Instance, often required by specific plugins.

Returns: A [Pipeline Instance Object](api-response-objects#pipeline-instance).

<h3 id="ctm-install-add-on" title="Permalink">ctm-install-add-on&nbsp;<a href="#ctm-install-add-on" style="display: margin-left: 1em;">&para;</a></h3>


Installs an Add-On from the VS-Exchange

Returns success or an error message.

    REQUIRED PARAMETERS
        -n,--name                The name of the add-on to install from the
                                      VS-Exchange
    OPTIONAL PARAMETERS
        -t,--team                The name of the team in which to install
                                      any projects, packages, pipelines, and
                                      tasks included in this add-on.
                                      Required if any any projects, packages,
                                      pipelines, or tasks exist in the add-on

#### Associated API: **install\_add\_on**

Installs an Add-On from the vs-exchange

Required Arguments:

* `name` - Name of the Add-On to install.

Optional Arguments:

* `team` - Team to which to add parts of the Add-On that are scoped to a team. Required if the Add-On contains any such parts.

Returns: `success` on success, errors otherwise.

<h3 id="ctm-install-license" title="Permalink">ctm-install-license&nbsp;<a href="#ctm-install-license" style="display: margin-left: 1em;">&para;</a></h3>


Installs or updates the Agility Connect/Continuum license by importing a license file

    REQUIRED PARAMETERS
        -i,--inputfile           Path to a license.dat file.
**Examples**

    ctm-install-license -i "~/license.lic"


#### Associated API: **install\_license**

Installs a license file.

Required Arguments:

* `license` - The text of a license key provided by Continuum.

Returns: Success or Error message.

<h3 id="ctm-invoke-plugin" title="Permalink">ctm-invoke-plugin&nbsp;<a href="#ctm-invoke-plugin" style="display: margin-left: 1em;">&para;</a></h3>


Execute a specified Flow Plugin Function

Response varies based on the specified Plugin.

    REQUIRED PARAMETERS
        -p,--plugin              Plugin.Module containing the desired
                                      function to invoke. (ex: github.main)
        -m,--method              Method to invoke. (ex "get_issue")
    OPTIONAL PARAMETERS
        -a,--args                A JSON object containing Plugin Function
                                      specific arguments.
        -t,--team                The Team to search for the Plugin Instance
                                      to use when invoking a Plugin Function
                                      that requires an Instance. Defaults to
                                      plugins available to All Teams.

#### Associated API: **invoke\_plugin**

Invoke a Plugin Function.

Required Arguments:

* `plugin` - The name of the Plugin PLUS the Module. (ex: github.main)
* `method` - The method to invoke. (ex "get_issue")

Optional Arguments:

* `args` - A JSON formatted string of arguments which will be sent to the Plugin Function.
* `team` - The Team in which to search for the Plugin Instance to use when invoking a Plugin Function that requires an Instance.
           Defaults to Plugins available to All Teams.
* `instance_name` - A named Plugin instance in the Continuum configuration.
                    Defaults to the Plugin Instance marked as default either within the specified Team or All Teams.
* `timeout` - The number of seconds to wait for the Plugin Function to execute before returning a timeout error.
              Defaults to 60 seconds.

> This API call will block the thread while it waits for the Plugin Function to execute. Therefore, the timeout argument
  should be kept reasonably small based on the Plugin Function being executed to reduce the amount of time the thread
  remains blocked.
> This API cannot invoke Pipeline Step Plugin Functions. Pipeline Step Plugin Functions require the context of a Step
  to run successfully.

Returns: Response varies depending on the Plugin Function called.

<h3 id="ctm-list-add-ons" title="Permalink">ctm-list-add-ons&nbsp;<a href="#ctm-list-add-ons" style="display: margin-left: 1em;">&para;</a></h3>


Lists all Add-Ons installed in this Continuum instance.

Returns: A list of Add-On details.

    OPTIONAL PARAMETERS
        -c,--include_contents    If true, lists the names of all parts of
                                      each of the Add-Ons. Defaults to false

#### Associated API: **list\_add\_ons**

Lists all Add-Ons installed in this Continuum instance.

Optional Arguments:

* `include_contents` - If true, lists the names of all parts of each of the Add-Ons. Defaults to false

Returns: A list of Add-On details.

<h3 id="ctm-list-canvas-items" title="Permalink">ctm-list-canvas-items&nbsp;<a href="#ctm-list-canvas-items" style="display: margin-left: 1em;">&para;</a></h3>


Lists Canvas Items

    OPTIONAL PARAMETERS
        -p,--project             Filter by a single Canvas Project.
        -c,--component           Further filter a Project by Component.
                                      (project is required.)
        -r,--repository          Specify either "file" or "db" repository.
                                      ("db" if omitted)

#### Associated API: **list\_canvas\_items**

Returns a list of all elements in the Canvas feature.

Optional Arguments:

* `project` - filter by a Canvas Project name.
* `component` - filter by a Canvas Component. (Project is required.)
* `repository` - specify the repository ('file' or 'db', 'db' if omitted.)

Returns: A list of all Canvas elements.

<h3 id="ctm-list-changes" title="Permalink">ctm-list-changes&nbsp;<a href="#ctm-list-changes" style="display: margin-left: 1em;">&para;</a></h3>


Lists all Changes.

    OPTIONAL PARAMETERS
        -r,--project             Limit the results to a specific project.
        -g,--group               Limit the results to a specific group.
        -s,--since               Limit the results to changes after the
                                      provided timestamp.
        -m,--managed             List only the managed changes.
        -u,--unmanaged           List only the unmanaged changes, Ignored
                                      if managed flag is provided
**Examples**

    ctm-list-changes


#### Associated API: **list\_changes**

Lists all Changes.

Optional Arguments:

* `project` - will limit the results to a specific 'project'.
* `group` - will limit the results to a specific 'group'.
* `since` - will only return changes since the provided timestamp.
* `managed` - will list only the managed changes.
* `unmanaged` - will list only the unmanaged changes.
* `limit` - will limit the number of changes.

Returns: A list of [Changes](restapi/api-response-objects.html#Changes){:target="robjs"}.

<h3 id="ctm-list-cloud-accounts" title="Permalink">ctm-list-cloud-accounts&nbsp;<a href="#ctm-list-cloud-accounts" style="display: margin-left: 1em;">&para;</a></h3>


Lists Cloud Accounts.

    OPTIONAL PARAMETERS
        -f,--filter              A string to use to filter the resulting
                                      data. Any row of data that has one field
                                      contains the string will be returned.
**Examples**

_List all cloud accounts with AWS in the name or cloud type_

    ctm-list-cloud-accounts -f "AWS"


#### Associated API: **list\_cloud\_accounts**

Lists all Cloud Accounts.

Optional Arguments: 

* `filter` - will filter a value match on:  (Multiple filter arguments can be provided, delimited by spaces.)

    * Account Name
    * Account Number
    * Provider
    * Login ID
    * Default Cloud Name

Returns: A list of [Cloud Account Objects](api-response-objects#cloud-account).

<h3 id="ctm-list-clouds" title="Permalink">ctm-list-clouds&nbsp;<a href="#ctm-list-clouds" style="display: margin-left: 1em;">&para;</a></h3>


Lists Cloud endpoints.

    OPTIONAL PARAMETERS
        -f,--filter              A string to use to filter the resulting
                                      data. Any row of data that has one field
                                      contains the string will be returned.
**Examples**

_List all cloud endpoints_

    ctm-list-clouds

_List all vcloud cloud endpoints_

    ctm-list-clouds -f "vCloud"


#### Associated API: **list\_clouds**

Lists all Clouds.

Optional Arguments: 

* `filter` - will filter a value match on:  (Multiple filter arguments can be provided, delimited by spaces.)

    * Cloud Name
    * Provider
    * Default Account Name
    * API URL

Returns: A list of [Cloud Objects](api-response-objects#cloud).

<h3 id="ctm-list-commands" title="Permalink">ctm-list-commands&nbsp;<a href="#ctm-list-commands" style="display: margin-left: 1em;">&para;</a></h3>

Lists all installed ctm-* commands.  Accepts no arguments.

<h3 id="ctm-list-packages" title="Permalink">ctm-list-packages&nbsp;<a href="#ctm-list-packages" style="display: margin-left: 1em;">&para;</a></h3>


Lists all Package Definitions.

    OPTIONAL PARAMETERS
        -f,--filter              A filter.
        -l,--limit               The number of packages to retrieve.
                                      Default limit is 100.
**Examples**

_List all Package Definitions

    ctm-list-packages


#### Associated API: **list\_packages**

Lists all Package Definitions.

Returns: A list of [Package Definition Objects](api-response-objects#package-definition).

<h3 id="ctm-list-pipelinegroups" title="Permalink">ctm-list-pipelinegroups&nbsp;<a href="#ctm-list-pipelinegroups" style="display: margin-left: 1em;">&para;</a></h3>


Lists all Pipeline Instance Groups.

    OPTIONAL PARAMETERS
        -p,--pipeline            Limit the results to a specific Pipeline.
        -r,--project             Limit the results to a specific project.
        -g,--group               Limit the results to a specific group.
**Examples**

_List all Pipeline Instance Groups

    ctm-list-pipelinegroups


#### Associated API: **list\_pipelinegroups**

Lists all Pipeline Instance Groups (Stories).

Optional Arguments:

* `pipeline` - will limit the results a specific Pipeline Definition.
* `project` - will limit the results a specific 'project'.
* `group` - will limit the results to a specific 'group'.

Returns: A list of [Pipeline Instance Group Objects](api-response-objects#pipeline-instance-group).

<h3 id="ctm-list-pipelineinstances" title="Permalink">ctm-list-pipelineinstances&nbsp;<a href="#ctm-list-pipelineinstances" style="display: margin-left: 1em;">&para;</a></h3>


Lists all Pipeline Instances.

    OPTIONAL PARAMETERS
        -d,--definition          Limit the results to a specific Pipeline
                                      Definition.
        -r,--project             Limit the results to a specific project.
        -g,--group               Limit the results to a specific group.
        -s,--since               Limit the results to Instances after the
                                      provided timestamp.
        -l,--limit               Limit the number of results.  (0 for all
                                      results, 100 if omitted.
**Examples**

_List all Pipeline Instances

    ctm-list-pipelineinstances


#### Associated API: **list\_pipelineinstances**

Lists all Pipeline Instances.

Optional Arguments:

* `definition` - will limit the results a specific Pipeline Definition.
* `project` - will limit the results to a specific 'project'.
* `group` - will limit the results to a specific 'group'.
* `since` - Will only return instances since the provided timestamp.
* `limit` - Limit the number of results.  (0 for all results, 100 if omitted.)

Returns: A list of [Pipeline Instance Objects](api-response-objects#pipeline-instance).

<h3 id="ctm-list-pipelines" title="Permalink">ctm-list-pipelines&nbsp;<a href="#ctm-list-pipelines" style="display: margin-left: 1em;">&para;</a></h3>


Lists all Pipeline Definitions.

    OPTIONAL PARAMETERS
        -f,--filter              A filter.
**Examples**

_List all Pipelines_

    ctm-list-pipelines


#### Associated API: **list\_pipelines**

Lists all Pipeline Definitions.

Returns: A list of [Pipeline Definition Objects](api-response-objects#pipeline-definition).

<h3 id="ctm-list-processes" title="Permalink">ctm-list-processes&nbsp;<a href="#ctm-list-processes" style="display: margin-left: 1em;">&para;</a></h3>


Lists server processes (poller, messenger, etc.) along with heartbeat information.

**Examples**

    ctm-list-processes


#### Associated API: **list\_processes**

Lists all running processes.

Returns: A list of [Process Objects](api-response-objects#process).

<h3 id="ctm-list-progressions" title="Permalink">ctm-list-progressions&nbsp;<a href="#ctm-list-progressions" style="display: margin-left: 1em;">&para;</a></h3>


Lists all Progressions.

    OPTIONAL PARAMETERS
        -f,--filter              A filter.
**Examples**

_List all Progressions

    ctm-list-progressions


#### Associated API: **list\_progressions**

Lists all Progressions.

Returns: A list of [Progression Objects](api-response-objects#progression.

<h3 id="ctm-list-projects" title="Permalink">ctm-list-projects&nbsp;<a href="#ctm-list-projects" style="display: margin-left: 1em;">&para;</a></h3>


Lists all Projects.

    OPTIONAL PARAMETERS
        -f,--filter              A filter.
**Examples**

_List all Projects

    ctm-list-projects


#### Associated API: **list\_projects**

Lists all Projects.

Optional Arguments:

Returns: A list of [Project Objects](api-response-objects#project).

<h3 id="ctm-list-tasks" title="Permalink">ctm-list-tasks&nbsp;<a href="#ctm-list-tasks" style="display: margin-left: 1em;">&para;</a></h3>


Lists Tasks

    OPTIONAL PARAMETERS
        -f,--filter              A string to use to filter the resulting
                                      data. Any row of data that has one field
                                      contains the string will be returned.
**Examples**

_List all tasks_

    ctm-list-tasks

_List all tasks with a particular string in the name

    ctm-list-tasks -f "Test Logging Level"


#### Associated API: **list\_tasks**

Lists all Tasks..

Optional Arguments:

* `filter` - will filter a value match in Task Name, Code or Description.  (Multiple filter arguments can be provided, delimited by spaces.)

Returns: A list of [Task Objects](api-response-objects#task).

> The Task Objects returned to this function are streamlined - they do not contain all the properties available in the `get_task` endpoint.

<h3 id="ctm-list-users" title="Permalink">ctm-list-users&nbsp;<a href="#ctm-list-users" style="display: margin-left: 1em;">&para;</a></h3>


Lists Users, Authentication type will be set to SSO if SSO is enabled in this instance

    OPTIONAL PARAMETERS
        -f,--filter              A string to use to filter the resulting
                                      data. Any row of data that has one field
                                      contains the string will be returned.
**Examples**

_List all users_

    ctm-list-users

_List all users with Administrator role_

    ctm-list-users -f "Administrator"


#### Associated API: **list\_users**

Lists all registered Users.

Optional Arguments:

* `filter` - will filter a value match on: (Multiple filter arguments can be provided, delimited by spaces.)

    * Full Name
    * Login ID
    * Role
    * Email address

Returns: A list of [User Objects](api-response-objects#user).

<h3 id="ctm-override-control" title="Permalink">ctm-override-control&nbsp;<a href="#ctm-override-control" style="display: margin-left: 1em;">&para;</a></h3>


Given a Package Revision, a Phase and a Control Name, will override that Control if it exists and is failed.

Returns: `success` on success, errors otherwise.

    REQUIRED PARAMETERS
        -p,--package             Name of Package
        -h,--phase               Phase containing the Activity/Control to
                                      override..
        -a,--activity            Name of Activity
        -c,--control             Name of Control.
        -e,--reason              Reason for overriding the Control.
    OPTIONAL PARAMETERS
        -r,--revision            Revision of Package containing the
                                      Control. (Takes precedence over
                                      "fullversion" if both are provided.)
        -f,--full_version        Full Version label of the Package
                                      containing the Control.

#### Associated API: **override\_control**

Given a Package Revision, a Phase and a Control Name, will override that Control if it exists and is failed.

Required Arguments:

* `package` - Name of the Package to promote to a progression Phase.
* `revision` - Revision number of a Package to promote, takes precedence over `full_version`.
* `full_version` - Full Version of package to promote, optional alternative selector to `revision`.
* `phase` - Name of the Phase containing the Activity of the Control to override.
* `activity` - Name of the Activity containing the Control to override.
* `control` - Name of the Control to override.
* `reason` - Description of the reason for overriding the Control.

Returns: `success` on success, errors otherwise.

<h3 id="ctm-powershell" title="Permalink">ctm-powershell&nbsp;<a href="#ctm-powershell" style="display: margin-left: 1em;">&para;</a></h3>


Test WinRM connections and issue commands.

    OPTIONAL PARAMETERS
        -s,--server              Windows server address.
        -u,--user                Windows User with WinRM permissions.
        -p,--password            Windows User Password.
        -a,--asset               The ID or Name of an Asset to use instead
                                      of --server, --user and --password.
        -k,--kerberos            Use Kerberos (Domain) authentication.
        -c,--command             A command to execute via WinRM.
**Examples**

    ctm-powershell -uusername -ppassword -sserver -c"write-host 'Hello World'"


#### Associated API: **winrm\_command**

#INTERNAL
Test connectivity or issue Windows Remote Management commands on a defined Asset.

Required Arguments:

* asset - Asset ID or Name of an Asset to use for the connection.

**OR**

* server - WinRM Server FQDN or IP address.
* user - User account.
* password - User password.


Optional Arguments:

* kerberos - Use Kerberos authentication if 'True', basic authentication if omitted.
* command - The command to execute.  (Will connection test only if omitted.)
* powershell - (boolean) If True, will execute the command as a PowerShell command.

Returns: The result of the command, or errors.

<h3 id="ctm-promote-revision" title="Permalink">ctm-promote-revision&nbsp;<a href="#ctm-promote-revision" style="display: margin-left: 1em;">&para;</a></h3>


Promotes a Package Revision to a particular Phase.

    REQUIRED PARAMETERS
        -p,--package             Name of the Package to promote to a
                                      Progression Phase.
        -h,--phase               Name of the Phase to which the specified
                                      Package Revision will be promoted.
    OPTIONAL PARAMETERS
        -r,--revision            Revision number of a Package to promote,
                                      takes precedence over "full_version".
        -f,--full_version        Optional Full Version of package to
                                      promote, optional alternative selector to
                                      "revision".
        -v,--new_version         Optional "new version" for this and all
                                      prior revisions of this Package.
**Examples**

    ctm-promote-revision -p "Some Package Name" -r 205 -h "Regression Testing"

    - or -

    ctm-promote-revision -p "Some Package Name" -f "15.2.3.205" -h "Regression Testing"


#### Associated API: **promote\_revision**

Promotes a Package Revision to a particular Phase.

Required Arguments:

* `package` - Name of the Package to promote to a Progression Phase.
* `revision` - Revision number of a Package to promote, takes precedence over `full_version`.
* `full_version` - Optional Full Version of package to promote, optional alternative selector to `revision`.
* `phase` - Name of the Phase to which the specified Package Revision will be promoted.

Optional Arguments:

* `new_version` - If provided, all Revisions being promoted will be updated to the provided `new_version`.  (Will attempt to also update `full_version` if possible.)

Returns: `success` on success, errors otherwise.

<h3 id="ctm-register-artifact" title="Permalink">ctm-register-artifact&nbsp;<a href="#ctm-register-artifact" style="display: margin-left: 1em;">&para;</a></h3>


Record a new revision of a specific Artifact.

    REQUIRED PARAMETERS
        -p,--project             Name or ID of the Project where this
                                      Artifact is defined.
        -n,--name                Name of the Artifact to revise.
        -b,--branch              Branch in the repository from which this
                                      artifact was built.
    OPTIONAL PARAMETERS
        -v,--version             Optional version identifier for this
                                      Artifact Revision.
        -l,--location            Optional location where this Artifact
                                      Revision can be found.
        -d,--build_data          Optional JSON object additional data about
                                      the build.
**Examples**

    ctm-register-artifact -p "My Project" -n "Artifact One" -l "path/to/artifact" -b master


#### Associated API: **register\_artifact**

Record a new revision of a specific Artifact.

Required Arguments:

* `project` - Name or ID of the Project where this Artifact is defined.
* `name` - Name of the Artifact to revise.
* `branch` - Branch in the repository from which this artifact was built.
* `location` - Optional URL or path to where this Artifact can be found.
* `build_data` - Optional JSON object additional data about the build.

Returns: `success` on success, errors otherwise.

<h3 id="ctm-remove-team-user" title="Permalink">ctm-remove-team-user&nbsp;<a href="#ctm-remove-team-user" style="display: margin-left: 1em;">&para;</a></h3>


Remove the specified User from a Team.

    REQUIRED PARAMETERS
        -t,--team                Name or ID of the Team to change.
        -u,--user                Name or ID of the User to remove.
    OPTIONAL PARAMETERS
        -d,--default             Users must be in at least one Team.  If
                                      the removal operation would leave this
                                      user Teamless, specify a new `Default`
                                      team for the User. Will attempt to use
                                      `Default` if omitted.
**Examples**

    ctm-remove-team-user -t "dev team" -u "bob"


#### Associated API: **remove\_team\_user**

Remove a User from a Team.

Only a 'Team Administrator' can manage Team membership.  If the credentials used for this API call
are not a Team Administrator for the specified Team, the call will not succeed.

Required Arguments:

* `team` - Name or ID of the Team to change.
* `user` - Name or ID of the User to remove.

Optional Arguments:

* `default` - Users must be in at least one Team.  If the removal operation would leave this User Teamless, specify a new default Team Name for the User. Will attempt to use `Default` if omitted.

> NOTE: if a new Default Team is assigned, the User will be given the `User` role in the Default Team

<h3 id="ctm-rerun-pipelineinstance" title="Permalink">ctm-rerun-pipelineinstance&nbsp;<a href="#ctm-rerun-pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>


Rerun an Instance, using the saved 'initial data'.

Returns a Pipeline Instance object.

    REQUIRED PARAMETERS
        -i,--pi                  Name or ID of a Pipeline Instance.

#### Associated API: **rerun\_pipelineinstance**

Rerun an Instance, using the saved 'initial data'.

This creates a new Instance exactly as the provided one was started.

Required Arguments:

* `pi` - The Name or ID of a Pipeline Instance.

Returns: A [Pipeline Instance Object](api-response-objects#pipeline-instance).
        
<h3 id="ctm-reset-password" title="Permalink">ctm-reset-password&nbsp;<a href="#ctm-reset-password" style="display: margin-left: 1em;">&para;</a></h3>


Resets a User's login password.

    OPTIONAL PARAMETERS
        -p,--password            The new password.
        -u,--user                The ID or Name of a User Account.
        -g,--generate            Generate a new, random password.
**Examples**

_Reset a User's password to a random password which will be emailed to the user_

    ctm-reset-password -u "username1" bob -g

_Reset a User's password to a specified password_

    ctm-reset-password -u "username1" -p "passw0rd"


#### Associated API: **reset\_password**

Resets the password of the authenticated, or a specified User.

If a user is specified, and the authenticated user is an Administrator,
this will reset the password of the specified user to the provided value.

If no user is specified, the password of the authenticated user will be changed.

> NOTE: to prevent accidental change of an Administrators password, an extra trap is in place: _the username (or id) MUST be provided, even if the authenticated user is the user being changed._

Required Arguments:

* `password` - the new password -or-
* `generate` - generate a random password.

Optional Arguments:

* `user` - Either the User ID or Name.

Returns: Success message if successful, error messages on failure.

<h3 id="ctm-resubmit-change" title="Permalink">ctm-resubmit-change&nbsp;<a href="#ctm-resubmit-change" style="display: margin-left: 1em;">&para;</a></h3>


Resubmits a previous change 'Submission' to the specified Project.

Identify the submission data using a valid MongoDB query.

For query syntax, see the MongDB find() syntax:
http://docs.mongodb.org/manual/reference/method/db.collection.find

Returns a success or failure.

    REQUIRED PARAMETERS
        -q,--query               A query in JSON format.
**Examples**

_To find a GitHub Webhook using the 'after' property:_

    ctm-resubmit-change -q '{"after" : "abc123"}'


#### Associated API: **resubmit\_change**

Resubmits a change 'Submission' payload to the specified Project.

Required Arguments:

* `query` - Valid MongoDB query to identify the previous payload to resubmit.

> If the query would return multiple submissions, the newest one is matched.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-retry-pipelineinstance" title="Permalink">ctm-retry-pipelineinstance&nbsp;<a href="#ctm-retry-pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>


Retries a failed or canceled Pipeline Instance.

Returns a Pipeline Instance object.

    REQUIRED PARAMETERS
        -i,--pi                  Name or ID of a Pipeline Instance.

#### Associated API: **retry\_pipelineinstance**

Attempt to retry a failed Pipeline Instance.  Simply restarts it again at Phase One.

CAUTION: The Workspace data is not cleared or reset.  Depending on the design of the Pipeline,
this may not succeed, or might produce unexpected results.

Required Arguments:

* `pi` - The Name or ID of a Pipeline Instance.

Returns: A [Pipeline Instance Object](api-response-objects#pipeline-instance).

<h3 id="ctm-reversion-packagerevision" title="Permalink">ctm-reversion-packagerevision&nbsp;<a href="#ctm-reversion-packagerevision" style="display: margin-left: 1em;">&para;</a></h3>


Changes the Version of the specified (and all matching previous) Package Revisions.

    REQUIRED PARAMETERS
        -p,--package             Name of the Package to promote to a
                                      Progression Phase.
        -v,--new_version         Optional "new version" for this and all
                                      prior revisions of this Package.
    OPTIONAL PARAMETERS
        -r,--revision            Revision number of a Package to promote,
                                      takes precedence over "full_version".
        -f,--full_version        Optional Full Version of package to
                                      promote, optional alternative selector to
                                      "revision".
**Examples**

    ctm-reversion-packagerevision -p "Some Package Name" -r 205 -v 15.1

    - or -

    ctm-promote-revision -p "Some Package Name" -f "15.2.3.205" -v 15.1


#### Associated API: **reversion\_packagerevision**

Changes the Version of the specified (and all matching previous) Package Revisions.

Required Arguments:

* `package` - Name of the Package to promote to a Progression Phase.
* `revision` - Revision number of a Package to promote, takes precedence over `full_version`.
* `full_version` - Optional Full Version of package to promote, optional alternative selector to `revision`.
* `new_version` - If provided, all Revisions being promoted will be updated to the provided `new_version`.  (Will attempt to also update `full_version` if possible.)

Returns: `success` on success, errors otherwise.

<h3 id="ctm-run-task" title="Permalink">ctm-run-task&nbsp;<a href="#ctm-run-task" style="display: margin-left: 1em;">&para;</a></h3>


Submits a Task for execution

    REQUIRED PARAMETERS
        -t,--task                The ID or Name of the Task to run.
    OPTIONAL PARAMETERS
        -l,--log_level           An optional Logging level.  One of 10,20
                                      (default),30,40,50 with 10 most verbose,
                                      50 no logging
        -o,--options             A JSON object containing additional
                                      options for the Task.
        -r,--run_later           The Task will be scheduled to run at the
                                      specified date/time.  ex. "7/4/1776
                                      15:30".
        -p,--parameters          JSON or XML formatted parameters, or a
                                      path to a file containing JSON or XML
                                      parameters.
        -i,--initialdata         JSON object initial runtime data, or a
                                      path to a file containing a JSON object.
**Examples**

_To submit a particular task_

    ctm-run-task -t "mytask01"

_To submit a task the most verbose logging level_

    ctm-run-task -t "mytask01" -l 10

_To submit a task logging on critical errors only_

    ctm-run-task -t "mytask01" -l 50

_To submit a task to run one time in the future_

    ctm-run-task -t "mytask01" -r "1/16/2014 9:40"

_Initial runtime data as a JSON string. (Notice double quotes inside, single quote outside.)_

    ctm-run-task -t "mytask01" -d '{"ship":"Serenity","captain":"Malcolm Reynolds"}'

_Initial runtime data in a JSON file_

    ctm-run-task -t "mytask01" -d "~/mytask01_params.json"



#### Associated API: **run\_task**

Runs a Task.

Required Arguments:

* `task` - Either the Task ID or Name.

Optional Arguments:

* `initialdata` - A JSON document defining the intial Runtime Variable environment for this Task.
* `log_level` - an integer (0-4) where 0 is none, 2 is normal and 4 is verbose.  Default is 2.
* `parameters` - A JSON or XML document defining parameters for the Task.
* `options` - a JSON object defining certain options for this Task.  Typically used to provide scope for extensions to the Task Engine.
* `run_later` - if provided, the Task will be scheduled to run at the specified date/time.  ex. "7/4/1776 15:30"
* `run_on_worker` - if provided, the Task will be explicitly assigned to the specified worker.  (Use the 'user@host' format to identify the target worker.)"

Returns: A [Task Instance Object](api-response-objects#task-instance).

* If 'output_format' is set to 'text', returns only a Task Instance ID.
* If 'run_later' was specified, will return a success or error message.

<h3 id="ctm-schedule-tasks" title="Permalink">ctm-schedule-tasks&nbsp;<a href="#ctm-schedule-tasks" style="display: margin-left: 1em;">&para;</a></h3>


Schedules one or more Tasks using a json template file.

    REQUIRED PARAMETERS
        -s,--schedulefile        The path to a json formatted schedule
                                      definition file. See the schedule_tasks
                                      API documentation for the format of the
                                      file.
**Examples**

    ctm-schedule-tasks -s ./schedule_template.json


#### Associated API: **schedule\_tasks**

Schedules one or more Tasks.

Required Arguments:

* `tasks` - a JSON document containing a list of Tasks and schedule details.

Schedule definition format:

> All lists are _zero based_ integers.

> The [Task Schedule Object](api-response-objects#task-schedule) response from the `get_task_schedules` command in JSON format
 can provide schedule definition examples for this command.

    [
        {
            "Task" : *task name*,
            "Version" : *optional*,
            "Months": "*" or [list of months],
            "DaysOrWeekdays": "Days" = days of the month, "Weekdays" = days of the week (default),
            "Days": "*" or [list of days],
            "Hours": "*" or [list of hours],
            "Minutes": "*" or [list of minutes]
        },
        {
            ...
        }
    ]

Returns: Nothing if successful, error messages on failure.

<h3 id="ctm-send-message" title="Permalink">ctm-send-message&nbsp;<a href="#ctm-send-message" style="display: margin-left: 1em;">&para;</a></h3>


Sends a message to an email address using the messenger.

    REQUIRED PARAMETERS
        -t,--to                  Comma-separated Users or addresses.
        -s,--subject             Subject of the message.
        -m,--message             Content of the message.
    OPTIONAL PARAMETERS
        -c,--cc                  Comma-separated Users or addresses to CC.
        -b,--bcc                 Comma-separated Users or addresses to BCC.
**Examples**

_To send an email to an email address_

    ctm-send-message -t "bob.thomas@example.com" -s "hello world" -m "this is a test message"

_To send an email to a list of email addresses with a blind copy_

    ctm-send-message -t "bob.thomas@example.com,tom.thumb@example.com" -b "hellen.hunt@example.com -s "hello world" -m "this is a test message"


#### Associated API: **send\_message**

Sends a message to a registered user.  Message will be 'From' the authenticated API user.

The 'to' argument accepts both email addresses AND Continuum Users.  Each item in the 'to' list
will try to look up a Continuum User, and if it doesn't match, will assume the entry is an email address.

Required Arguments:

* `to` - a single or comma-separated list of valid email addresses or Continuum Users.
* `subject` - a subject line
* `message` - the message body

Optional Arguments:

* `cc` - a carbon copy list of comma-separated email addresses or Continuum Users.
* `bcc` - a blind carbon copy list of comma-separated email addresses or Continuum Users.

Returns: Success message if successful, error message on failure.

<h3 id="ctm-set-pi-description" title="Permalink">ctm-set-pi-description&nbsp;<a href="#ctm-set-pi-description" style="display: margin-left: 1em;">&para;</a></h3>


Sets pipeline instance description

    REQUIRED PARAMETERS
        -i,--pi                  Pipeline instance ID or name
        -d,--description         Key name to set

#### Associated API: **set\_pi\_description**

Set the description of a specific Pipeline Instance

Required Arguments:

* `pi` - the id or name of a Pipeline Instance
* `description` - Description to set (HTML allowed)

Returns: 'true' on success, errors on failure.

<h3 id="ctm-set-pi-global-summary" title="Permalink">ctm-set-pi-global-summary&nbsp;<a href="#ctm-set-pi-global-summary" style="display: margin-left: 1em;">&para;</a></h3>


Sets pipeline instance global summary data

    REQUIRED PARAMETERS
        -i,--pi                  Pipeline instance ID or name
        -k,--key                 Key name to set
        -v,--value               Value to set

#### Associated API: **set\_pi\_global\_summary**

Set global summary data on a pipeline instance

Required Arguments:

* `pi` - the id or name of a pipeline instance
* `key` - key to set in the global summary
* `value` - value for the provided key

Returns: 'true' on success, errors on failure.

Example using curl:

    curl http://continuum-server.example.com:8080/api/set_pi_data?token=5752fb9abb288013973fabf4&key=hello&value=world&pi=57acb49a320c7a41bf32958a


<h3 id="ctm-set-pipelinegroup-number" title="Permalink">ctm-set-pipelinegroup-number&nbsp;<a href="#ctm-set-pipelinegroup-number" style="display: margin-left: 1em;">&para;</a></h3>


Set the autonumber root on Pipeline Instance Group. (Used to issue ascending numbers to Instances in the Group.)

Requires the '_id' of the Pipeline Instance Group and the new number value to set.

Returns success or failure.

    REQUIRED PARAMETERS
        -i,--pg                  ID of a Pipeline Instance Group.
        -n,--newnumber           New Number to set.

#### Associated API: **set\_pipelinegroup\_number**

Set the autonumber root on Pipeline Instance Group. (Used to issue ascending numbers to Instances in the Group.)

Required Arguments:

* `pg` - The ID of a Pipeline Instance Group.
* `newnumber` - The new number to set as the autonumber root.

Returns: 'true' on success, errors on failure.

<h3 id="ctm-stop-task" title="Permalink">ctm-stop-task&nbsp;<a href="#ctm-stop-task" style="display: margin-left: 1em;">&para;</a></h3>


Cancels a task instance in a runnning status

    REQUIRED PARAMETERS
        -i,--instance            The Task Instance ID to stop.
**Examples**

    ctm-stop-task -i 43675


#### Associated API: **stop\_task**

Stops a running Task Instance.

Required Arguments:

* `instance` - The Task Instance identifier.

Returns: Nothing if successful, error messages on failure.

<h3 id="ctm-test-messagehub" title="Permalink">ctm-test-messagehub&nbsp;<a href="#ctm-test-messagehub" style="display: margin-left: 1em;">&para;</a></h3>


Sends a test alert message to the UI.

    REQUIRED PARAMETERS
        -s,--server              URL of the Agility Connect/Continuum
                                      server.  Use "wss" if server is running in
                                      SSL mode, otherwise use "ws".  Use the
                                      port as configured, or the default of
                                      8083.
**Examples**

_To send an email to an email address_

    ctm-test-messagehub -u ws://10.0.0.1:8083


<h3 id="ctm-testbamboo" title="Permalink">ctm-testbamboo&nbsp;<a href="#ctm-testbamboo" style="display: margin-left: 1em;">&para;</a></h3>


Test Bamboo connectivity

    OPTIONAL PARAMETERS
        -i,--instance            Bamboo instance name in the Continuum
                                      configuration. Optional, do not use if
                                      testing default Bamboo instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testbamboo -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testbitbucket" title="Permalink">ctm-testbitbucket&nbsp;<a href="#ctm-testbitbucket" style="display: margin-left: 1em;">&para;</a></h3>


Test BitBucket connectivity

    OPTIONAL PARAMETERS
        -i,--instance            Instance name in the Continuum
                                      configuration. Optional, not necessary if
                                      testing the default instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testbitbucket -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testgitlab" title="Permalink">ctm-testgitlab&nbsp;<a href="#ctm-testgitlab" style="display: margin-left: 1em;">&para;</a></h3>


Test GitLab connectivity

    OPTIONAL PARAMETERS
        -i,--instance            Instance name in the Continuum
                                      configuration. Optional, not necessary if
                                      testing the default instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testgitlab -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testhipchat" title="Permalink">ctm-testhipchat&nbsp;<a href="#ctm-testhipchat" style="display: margin-left: 1em;">&para;</a></h3>


Test HipChat Server connectivity

    OPTIONAL PARAMETERS
        -i,--instance            HipChat instance name in the Continuum
                                      configuration. Optional, do not use if
                                      testing default HipChat instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testhipchat -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testjenkins" title="Permalink">ctm-testjenkins&nbsp;<a href="#ctm-testjenkins" style="display: margin-left: 1em;">&para;</a></h3>


Test Jenkins connectivity

    OPTIONAL PARAMETERS
        -i,--instance            Jenkins instance name in the Continuum
                                      configuration. Optional, do not use if
                                      testing default Jenkins instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testjenkins -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testjira" title="Permalink">ctm-testjira&nbsp;<a href="#ctm-testjira" style="display: margin-left: 1em;">&para;</a></h3>


Test Jira connectivity

    OPTIONAL PARAMETERS
        -i,--instance            Jira instance name in the Continuum
                                      configuration. Optional, do not use if
                                      testing default Jira instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testjira -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testoctopus" title="Permalink">ctm-testoctopus&nbsp;<a href="#ctm-testoctopus" style="display: margin-left: 1em;">&para;</a></h3>


Test Octopus connectivity

    OPTIONAL PARAMETERS
        -i,--instance            Octopus instance name in the Continuum
                                      configuration. Optional, do not use if
                                      testing default Octopus instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testoctopus -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testopenshift" title="Permalink">ctm-testopenshift&nbsp;<a href="#ctm-testopenshift" style="display: margin-left: 1em;">&para;</a></h3>


Test OpenShift connectivity

    OPTIONAL PARAMETERS
        -i,--instance            Instance name in the Continuum
                                      configuration. Optional, not necessary if
                                      testing the default instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testopenshift -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testsonarqube" title="Permalink">ctm-testsonarqube&nbsp;<a href="#ctm-testsonarqube" style="display: margin-left: 1em;">&para;</a></h3>


Test Sonarqube connectivity

    OPTIONAL PARAMETERS
        -i,--instance            Sonarqube instance name in the Continuum
                                      configuration. Optional, do not use if
                                      testing default Sonarqube instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testsonarqube -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testteamcity" title="Permalink">ctm-testteamcity&nbsp;<a href="#ctm-testteamcity" style="display: margin-left: 1em;">&para;</a></h3>


Test TeamCity connectivity

    OPTIONAL PARAMETERS
        -i,--instance            TeamCity instance name in the Continuum
                                      configuration. Optional, do not use if
                                      testing default TeamCity instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testteamcity -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-testversionone" title="Permalink">ctm-testversionone&nbsp;<a href="#ctm-testversionone" style="display: margin-left: 1em;">&para;</a></h3>


Test VersionOne connectivity

    OPTIONAL PARAMETERS
        -i,--instance            VersionOne instance name in the Continuum
                                      configuration. Optional, do not use if
                                      testing default VersionOne instance.
        -t,--team                The Team to search for the Plugin Instance
                                      to use. Defaults to plugins available to
                                      All Teams.
**Examples**

    ctm-testversionone -i instancename


#### Associated API: **test\_plugin\_connection**

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message

<h3 id="ctm-uninstall-add-on" title="Permalink">ctm-uninstall-add-on&nbsp;<a href="#ctm-uninstall-add-on" style="display: margin-left: 1em;">&para;</a></h3>


Uninstalls an Add-On from the VS-Exchange

Returns success or an error message.

    REQUIRED PARAMETERS
        -n,--name                The name of the Add-On to uninstall from
                                      Continuum

#### Associated API: **uninstall\_add\_on**

Uninstalls an Add-On from Continuum

Required Arguments:

* `name` - Name of the Add-On to uninstall.

Returns: `success` on success, errors otherwise.

<h3 id="ctm-untag-object" title="Permalink">ctm-untag-object&nbsp;<a href="#ctm-untag-object" style="display: margin-left: 1em;">&para;</a></h3>


Removes a security Tag from an object.

    REQUIRED PARAMETERS
        -t,--tag                 The name of the Tag.
        -o,--object_id           The ID of the object.
        -y,--object_type         The numeric object type of the object.
                                      (User = 1, Asset = 2, Task = 3)
**Examples**

_To untag a task using task uuid and the task object type_

    ctm-untag-object -t "development" -o "7f17e600-794f-11e3-bb4c-c8bcc89d4845" -y 3


#### Associated API: **remove\_object\_tag**

Removes a Tag from an object.

Required Arguments:

* `tag` - The name of the Tag.
* `object_id` - The ID of the object.
* `object_type` - The numeric type of the object.

Returns: Success message if successful, error message on failure.

<h3 id="ctm-update-user" title="Permalink">ctm-update-user&nbsp;<a href="#ctm-update-user" style="display: margin-left: 1em;">&para;</a></h3>


Updates a User account, Authentication type will be set to SSO if SSO is enabled in this instance

    REQUIRED PARAMETERS
        -u,--user                The ID or Name of a User account.
    OPTIONAL PARAMETERS
        -n,--name                The full name of the user.
        -r,--role                The users role.  (Valid values:
                                      Administrator, Developer, User)
                                      Valid Values: Administrator|Developer|User
        -t,--teams               A list of teams the user belongs to, along
                                      with a role for each team. Teams and roles
                                      are separated by a colon. Team/role pairs
                                      are separated by commas.
        --is-sys-admin           Whether the user should have system
                                      administrator privileges. (Valid values:
                                      True or False)
        --is-shared-asset-mgr    Whether the user should have shared asset
                                      manager privileges. (Valid values: True or
                                      False)
        -e,--email               Email address for the user.  Required if
                                      "password" is omitted.
        -a,--authtype            "local" or "ldap".  Default is "local" if
                                      omitted.
                                      Valid Values: local|ldap
        -f,--forcechange         Require user to change password. Default
                                      is "true" (1) if omitted. (Valid values: 0
                                      or 1).
                                      Valid Values: 0|1
        -s,--status              Status of the new account. Default is
                                      "enabled" if omitted. (Valid values:
                                      enabled, disabled, locked)
                                      Valid Values: enabled|disabled|locked
        -x,--expires             Expiration date for this account.  Must be
                                      in mm/dd/yyyy format.
        -g,--groups              A list of groups the user belongs to.
                                      Group names cannot contain spaces. Comma
                                      delimited list.
        -c,--contributors        Usernames in source control management
                                      systems related to an user. Comma
                                      delimited list.
        -p,--password            The new password.
        --generate               Generate a new, random password.
**Examples**

    ctm-update-user -u "dave.thomas" -s "disabled"  --force


#### Associated API: **update\_user**

Updates a user account.

Only an 'Administrator' can manage other users.  If the credentials used for this API call
are not an Administrator, the call will not succeed.

Properties will only be updated if the option is provided.  Omitted properties will not be changed.

NOTE: the "username" of a user cannot be changed.

If a user has 'locked' their account by numerous failed login attempts, the flag is reset
by setting any property.  It's easiest to just the status to 'enabled'.

Required Arguments:

* `user` - ID or Name of the User to update.

Optional Arguments:

* `name` - The full name of the user.
* `role` - The users role.  (Valid values: Administrator, Developer, User)
* `teams` - A list of teams the user belongs to, along with a role for each team. Teams and roles are separated by a
* `is_system_administrator` - Whether the user should have system administrator privileges. (Valid values: 'true' or 'false') Default is false.
* `is_shared_asset_manager` - Whether the user should have shared asset manager privileges. (Valid values: 'true' or 'false') Default is false.
* `email` - Email address for the user.  Can be cleared with "None".
* `authtype` - 'local' or 'ldap'.
* `forcechange` - Require user to change password on next login. (Valid values: 'true' or 'false')
* `status` - Status of the account. (Valid values: enabled, disabled, locked)
* `expires` - Expiration date for this account.  Must be in mm/dd/yyyy format. Can be cleared with "None".
* `groups` - Add to the list of groups the user belongs to. Group names cannot contain spaces. Comma delimited list.
* `contributors` - Contributors are usernames in source control management systems related to this User
                   (Enter one or more comma-separated Contributor 'aliases').
* `password` - the new password.
* - OR -
* `generate` - generate a random password.

Returns: A [User Object](api-response-objects#user).

<h3 id="ctm-version" title="Permalink">ctm-version&nbsp;<a href="#ctm-version" style="display: margin-left: 1em;">&para;</a></h3>


Displays the Version by request from the API.

**Examples**

    ctm-version


#### Associated API: **version**


Returns: The Continuum version.

<h3 id="ctm-winrm" title="Permalink">ctm-winrm&nbsp;<a href="#ctm-winrm" style="display: margin-left: 1em;">&para;</a></h3>


Test WinRM connections and issue commands.

    OPTIONAL PARAMETERS
        -s,--server              Windows server address.
        -u,--user                Windows User with WinRM permissions.
        -p,--password            Windows User Password.
        -a,--asset               The ID or Name of an Asset to use instead
                                      of --server, --user and --password.
        -k,--kerberos            Use Kerberos (Domain) authentication.
        -c,--command             A command to execute via WinRM.
**Examples**

    ctm-winrm -uusername -ppassword -sserver -c"dir c:"


#### Associated API: **winrm\_command**

#INTERNAL
Test connectivity or issue Windows Remote Management commands on a defined Asset.

Required Arguments:

* asset - Asset ID or Name of an Asset to use for the connection.

**OR**

* server - WinRM Server FQDN or IP address.
* user - User account.
* password - User password.


Optional Arguments:

* kerberos - Use Kerberos authentication if 'True', basic authentication if omitted.
* command - The command to execute.  (Will connection test only if omitted.)
* powershell - (boolean) If True, will execute the command as a PowerShell command.

Returns: The result of the command, or errors.

