# Digital.ai Continuum REST API

<h3 id="accept_webhook" title="Permalink">accept_webhook&nbsp;<a href="#accept_webhook" style="display: margin-left: 1em;">&para;</a></h3>

Accepts any JSON payload submitted, and runs it through the defined list of Directives.

Required Arguments:

* `handler` - name of a defined 'Webhook Handler' containing directives to apply to this payload.

Returns: Success message if successful, error message on failure.


<h3 id="add_cloud_keypair" title="Permalink">add_cloud_keypair&nbsp;<a href="#add_cloud_keypair" style="display: margin-left: 1em;">&para;</a></h3>

Adds a Key Pair to a Cloud.

Required Arguments: 

* `cloud` - Name or ID of the Cloud to update.
* `name` - a name for the Key Pair.
* `private_key` - the private key.

Optional Arguments: 

* `passphrase` - a passphrase for this Key Pair.
    
Returns: A list of [Cloud KeyPair Objects](api-response-objects#cloud-keypair).


<h3 id="add_object_tag" title="Permalink">add_object_tag&nbsp;<a href="#add_object_tag" style="display: margin-left: 1em;">&para;</a></h3>

Adds a security Tag to an object.

Required Arguments:

* `tag` - The name of the Tag.
* `object_id` - The ID of the object.
* `object_type` - The numeric type of the object.

Returns: Success message successful, error message on failure.

Valid and currently implemented `object_type` values are:

* `User` = 1
* `Asset` = 2
* `Task` = 3
* `Canvas Item` = 50


<h3 id="add_team_user" title="Permalink">add_team_user&nbsp;<a href="#add_team_user" style="display: margin-left: 1em;">&para;</a></h3>

Add a User to a Team.

Only a 'Team Administrator' can manage Team membership.  If the credentials used for this API call
are not a Team Administrator for the specified Team, the call will not succeed.

Required Arguments:

* `team` - Name or ID of the Team to change.
* `user` - Name or ID of the User to add.
* 'team_role' - Name of the Role for new user to adopt on new team



<h3 id="cancel_pipelineinstance" title="Permalink">cancel_pipelineinstance&nbsp;<a href="#cancel_pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>

Cancel a running Pipeline Instance.

All Pending or Processing statuses will be set to Canceled.

Required Arguments:

* `pi` - The Name or ID of a Pipeline Instance.

Returns: 'true' on success, errors on failure.


<h3 id="cancel_transformer_event" title="Permalink">cancel_transformer_event&nbsp;<a href="#cancel_transformer_event" style="display: margin-left: 1em;">&para;</a></h3>

 Cancel failed event

        Required Arguments:

        * `inbound_id` - The inbound id of the failed event
        

<h3 id="check_transformer_data_map_name_exists" title="Permalink">check_transformer_data_map_name_exists&nbsp;<a href="#check_transformer_data_map_name_exists" style="display: margin-left: 1em;">&para;</a></h3>

Check if a mapping name already exists.

        Required Arguments:

        * `name` - The mapping name to be checked for existence.

        Returns a boolean indicating if the mapping already exists.
        

<h3 id="complete_activity" title="Permalink">complete_activity&nbsp;<a href="#complete_activity" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="configure_plugin" title="Permalink">configure_plugin&nbsp;<a href="#configure_plugin" style="display: margin-left: 1em;">&para;</a></h3>

Configure a specific Flow Plugin.

Required Arguments:

* `plugin` - JSON object formatted as a valid config for the specified plugin.

> The following keys will be encrypted if provided: `token`, `password`.

Returns: success or error.


<h3 id="configure_plugin_instance" title="Permalink">configure_plugin_instance&nbsp;<a href="#configure_plugin_instance" style="display: margin-left: 1em;">&para;</a></h3>

Add a new instance for a particular plugin type. Note: does not overwrite existing instances.

Required Arguments:

* `plugin` - Plugin type.
* `name` - Name of new plugin instance.

Optional Arguments:
* `team` - Team with which to associate this plugin instance. Defaults to All Teams.

Conditional Arguments: The args passed in are dependent on the plugin type
specified in `plugin` arg. For most types they will be as they appear below,
some types have other naming conventions such as `api_token` instead of `password`.

* `url` - Server URL.
* `user` - LoginID for server.
* `password` - Password for server.
* `api_token` - API token for plugin instance. This will map to a value of "Token" in the ui and "token" in the database.

Returns: success or error.


<h3 id="configure_plugins" title="Permalink">configure_plugins&nbsp;<a href="#configure_plugins" style="display: margin-left: 1em;">&para;</a></h3>

None

<h3 id="copy_project" title="Permalink">copy_project&nbsp;<a href="#copy_project" style="display: margin-left: 1em;">&para;</a></h3>

Copy a Project.

Required Arguments:

* `project` - the id or name of a Project.
* `newname` - a name for the new Project.

Returns: 'true' on success, errors on failure.


<h3 id="create_account" title="Permalink">create_account&nbsp;<a href="#create_account" style="display: margin-left: 1em;">&para;</a></h3>


Creates a Cloud Account.

Required Arguments:
 
* `name` - a name for the new Account.
* `provider` - one of the valid cloud providers.
* `login` - the login id (access key) for this Account.
* `password` - a password (secret key) for this Account.
* `default_cloud` - the name of a default Cloud for this Account.

Optional Arguments: 

* `account_number` - an Account number.

Returns: The new [Cloud Account Object](api-response-objects#cloud-account).


<h3 id="create_asset" title="Permalink">create_asset&nbsp;<a href="#create_asset" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="create_canvas_item" title="Permalink">create_canvas_item&nbsp;<a href="#create_canvas_item" style="display: margin-left: 1em;">&para;</a></h3>

Creates a new Canvas item.

Required Arguments:

* `project` - a Canvas Project name.
* `component` - a Canvas Component name.
* `name` - a Canvas item name.
* `resourcedata` - the content of the item.

Optional Arguments:

* `ignoreconflicts` - if 'true' existing items will be overwritten.

Returns: Success or Error message.


<h3 id="create_cloud" title="Permalink">create_cloud&nbsp;<a href="#create_cloud" style="display: margin-left: 1em;">&para;</a></h3>

Creates a Cloud.

Required Arguments: 

* `name` - a name for the new Cloud.
* `provider` - one of the valid cloud providers.
* `apiurl` - URL of the Cloud API endpoint.
* `apiprotocol` - Cloud API endpoint protocol.

Optional Arguments:
 
* `default_account` - the name of a default Account for this Cloud.

Returns: The new [Cloud Object](api-response-objects#cloud).


<h3 id="create_credential" title="Permalink">create_credential&nbsp;<a href="#create_credential" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="create_data_map" title="Permalink">create_data_map&nbsp;<a href="#create_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Creat data map for assets.

Required Arguments:

* `name` - Name of mapping used to associate.
* `source` - Source system from which sync has to happen
* `destinations` - Destination systems to which the sync has to happen

Optional Arguments:

* `description` - Description of mapping.
* `projects` - List of project mappings across external systems.

Returns: Created ID or error message.


<h3 id="create_package" title="Permalink">create_package&nbsp;<a href="#create_package" style="display: margin-left: 1em;">&para;</a></h3>

Create a Package Definition.

Required Arguments:

* `name` - the name of a Package.
* `team` - Team to which the Package Definition should belong.

Optional Arguments:

* `description` - a description of the Package Definition.
* `progression` - a Progression to associate with the Package Definition.

Returns: A [Package Definition Object](api-response-objects#package-definition).


<h3 id="create_pipeline" title="Permalink">create_pipeline&nbsp;<a href="#create_pipeline" style="display: margin-left: 1em;">&para;</a></h3>

Create a Pipeline Definition.

Required Arguments:

* `template` - A JSON document formatted as a CSK Pipeline Definition.

Returns: A [Pipeline Definition Object](api-response-objects#pipeline-definition).


<h3 id="create_progression" title="Permalink">create_progression&nbsp;<a href="#create_progression" style="display: margin-left: 1em;">&para;</a></h3>

Create a Progression Definition.

Required Arguments:

* `name` - the name of a Progression.

Optional Arguments:

* `description` - a description of the Progression.

Returns: A [Progression Definition Object](api-response-objects#progression-definition).


<h3 id="create_project" title="Permalink">create_project&nbsp;<a href="#create_project" style="display: margin-left: 1em;">&para;</a></h3>

Create a Project.

Required Arguments:

* `name` - Name of the Project.
* `team` - Team which the Project belongs to.

Returns: A [Project Object](api-response-objects#project).


<h3 id="create_tag" title="Permalink">create_tag&nbsp;<a href="#create_tag" style="display: margin-left: 1em;">&para;</a></h3>

Creates a new Tag for grouping Users.

Required Arguments:

* `name` - The name of the new Tag.  (AlphaNumeric ONLY. Cannot contain spaces, punctuation or special characters.)

Optional Arguments:

* `description` - Describe the Tag.

Returns: The new [Tag Object](api-response-objects#tag) if successful, error message on failure.
    

<h3 id="create_task" title="Permalink">create_task&nbsp;<a href="#create_task" style="display: margin-left: 1em;">&para;</a></h3>

Create a new Task.

Required Arguments:

* `name` - a name for the new Task.
* `team` - Team which the task belongs to.

Optional Arguments:

* `code` - a Task code.
* `desc` - a Task description.

Returns: A [Task Object](api-response-objects#task).


<h3 id="create_task_from_json" title="Permalink">create_task_from_json&nbsp;<a href="#create_task_from_json" style="display: margin-left: 1em;">&para;</a></h3>

Create a new Task from a JSON Task backup document.

Required Arguments:

* `json` - A properly formatted JSON representation of a Task.

Returns: A [Task Object](api-response-objects#task).


<h3 id="create_team" title="Permalink">create_team&nbsp;<a href="#create_team" style="display: margin-left: 1em;">&para;</a></h3>

Create a new team

Only an 'Administrator' can create teams.  If the credentials used for this API call
are not an Administrator, the call will not succeed.

Required Arguments:

* `name` - A name for the new Team.

Optional Arguments:

* `description` - A description of the new Team.


<h3 id="create_transformer_data_map" title="Permalink">create_transformer_data_map&nbsp;<a href="#create_transformer_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Creates a new data map.

        Required Arguments:

        * `name` - The name of the data map.
        * `direction_type` - The direction of the mapping (forward-direction, backward-direction or bi-direction).
        * `forward-direction` - The field mappings for the forward direction.
        * `backward-direction` - The field mappings for the backward direction.

        Returns the id of the newly created data map.
        

<h3 id="create_user" title="Permalink">create_user&nbsp;<a href="#create_user" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="create_webhook" title="Permalink">create_webhook&nbsp;<a href="#create_webhook" style="display: margin-left: 1em;">&para;</a></h3>

Creates a new outbound Webhook configuration.

Required Arguments:

* `name` - The name of the Webhook configuration.
* `destinationurl` - The URL to which events will be posted.

Returns: Success message if successful, error message on failure.
    

<h3 id="delete_asset" title="Permalink">delete_asset&nbsp;<a href="#delete_asset" style="display: margin-left: 1em;">&para;</a></h3>

Deletes an Asset.

Required Arguments:

* `asset` - Either the Asset ID or Name.

Returns: Nothing if successful, error messages on failure.


<h3 id="delete_cloud_keypair" title="Permalink">delete_cloud_keypair&nbsp;<a href="#delete_cloud_keypair" style="display: margin-left: 1em;">&para;</a></h3>

Removes a Key Pair from a Cloud.

Required Arguments: 

* `cloud` - Name or ID of the Cloud.
* `name` - Name of the Key Pair to delete.
    
Returns: A list of [Cloud KeyPair Objects](api-response-objects#cloud-keypair).


<h3 id="delete_credential" title="Permalink">delete_credential&nbsp;<a href="#delete_credential" style="display: margin-left: 1em;">&para;</a></h3>

Removes a Shared Credential.

Required Arguments:

* `credential` - Name or ID of the Credential to delete.

Returns: Success message if successful, error message on failure.


<h3 id="delete_data_map" title="Permalink">delete_data_map&nbsp;<a href="#delete_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Delete data map.

Required Arguments:

* `mapping_id` - data mapping to delete

Returns: Success or error message.


<h3 id="delete_package" title="Permalink">delete_package&nbsp;<a href="#delete_package" style="display: margin-left: 1em;">&para;</a></h3>

Delete a Package Definition. Destructive of history, and there is no undo.

Required Arguments:

* `package` - the id or name of a Package.

Optional Arguments:

* `preserve` - If `true`, will delete all data but preserve the actual package definition. Valid values: true|false (default).

Returns: 'true' on success, errors on failure.


<h3 id="delete_pipeline" title="Permalink">delete_pipeline&nbsp;<a href="#delete_pipeline" style="display: margin-left: 1em;">&para;</a></h3>

Permanently delete a Pipeline Definition.

Required Arguments:

* `pipeline` - the id or name of a Pipeline Definition.

Returns: 'true' on success, errors on failure.


<h3 id="delete_pipelinegroup" title="Permalink">delete_pipelinegroup&nbsp;<a href="#delete_pipelinegroup" style="display: margin-left: 1em;">&para;</a></h3>

Permanently delete a Pipeline Instance Group.

> NOTE: at the moment, requires the '_id' of the Pipeline Instance Group.

Required Arguments:

* `pg` - The ID of a Pipeline Instance Group.

Returns: 'true' on success, errors on failure.


<h3 id="delete_pipelineinstance" title="Permalink">delete_pipelineinstance&nbsp;<a href="#delete_pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>

Permanently delete a Pipeline Instance.

Required Arguments:

* `pi` - The Name or ID of a Pipeline Instance.

Returns: 'true' on success, errors on failure.


<h3 id="delete_plan" title="Permalink">delete_plan&nbsp;<a href="#delete_plan" style="display: margin-left: 1em;">&para;</a></h3>

Deletes a specific queued execution Plan.

Required Arguments:

* `plan_id` - The integer ID of the Plan to delete.

Returns: Nothing if successful, error messages on failure.


<h3 id="delete_progression" title="Permalink">delete_progression&nbsp;<a href="#delete_progression" style="display: margin-left: 1em;">&para;</a></h3>

Delete a Progression Definition. Destructive of history, and there is no undo.

Required Arguments:

* `progression` - the id or name of a Progression.

Returns: 'true' on success, errors on failure.


<h3 id="delete_project" title="Permalink">delete_project&nbsp;<a href="#delete_project" style="display: margin-left: 1em;">&para;</a></h3>

Permanently delete a Project.

Required Arguments:

* `project` - the id or name of a Project.

Optional Arguments:

* `preserve` - If `true`, will delete all data but preserve the actual project. Valid values: true|false (default).

Returns: 'true' on success, errors on failure.


<h3 id="delete_registry" title="Permalink">delete_registry&nbsp;<a href="#delete_registry" style="display: margin-left: 1em;">&para;</a></h3>

Permanently delete a registry.

Required Arguments:

* `registry` - Name of the Registry document.

Returns: 'true' on success, errors on failure.


<h3 id="delete_schedule" title="Permalink">delete_schedule&nbsp;<a href="#delete_schedule" style="display: margin-left: 1em;">&para;</a></h3>

Deletes a Task Schedule and all queued execution Plans.

Required Arguments:

* `schedule_id` - The UUID of the Schedule to delete.

Returns: Nothing if successful, error messages on failure.


<h3 id="delete_tag" title="Permalink">delete_tag&nbsp;<a href="#delete_tag" style="display: margin-left: 1em;">&para;</a></h3>

Deletes a security Tag.

Required Arguments:

* `name` - The name of the Tag.

Returns: Success message if successful, error message on failure.


<h3 id="delete_task" title="Permalink">delete_task&nbsp;<a href="#delete_task" style="display: margin-left: 1em;">&para;</a></h3>

Deletes all versions of a Task.

Required Arguments:

* `task` - Either the Task ID or Name.

Optional Arguments:

* `force_delete` - Delete the Task, even if there are historical rows and references.  (Valid values: 1, yes, true)

Returns: Nothing if successful, error messages on failure.


<h3 id="delete_transformer_data_map" title="Permalink">delete_transformer_data_map&nbsp;<a href="#delete_transformer_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Delete the data map.

        Required Arguments:

        * `id` - The id of the data map.

        

<h3 id="delete_user" title="Permalink">delete_user&nbsp;<a href="#delete_user" style="display: margin-left: 1em;">&para;</a></h3>

Deletes a user account
Only an 'Administrator' can manage other users.  If the credentials used for this API call
are not an Administrator, the call will not succeed.

Properties will only be updated if the option is provided.  Omitted properties will not be changed.

NOTE: the "username" of a user cannot be changed.

If a user has 'locked' their account by numerous failed login attempts, the flag is reset
by setting any property.  It's easiest to just the status to 'enabled'.

Required Arguments:

* `user` - ID or Name of the User to update.

        

<h3 id="deliver_revision" title="Permalink">deliver_revision&nbsp;<a href="#deliver_revision" style="display: margin-left: 1em;">&para;</a></h3>

Delivers a Package Revision out of a Progression into a Delivered condition.

Required Arguments:

* `package` - Name of the Package.
* `revision` - Revision number of a Package to deliver, takes precedence over `full_version`.
* `full_version` - Optional Full Version of package to deliver, optional alternative selector to `revision`.

Returns: `success` on success, errors otherwise.


<h3 id="describe_task_parameters" title="Permalink">describe_task_parameters&nbsp;<a href="#describe_task_parameters" style="display: margin-left: 1em;">&para;</a></h3>

Describes the Parameters for a Task.

Required Arguments:

* `task` - Value can be either a Task ID, Code or Name.

Optional Arguments:

Returns: A help document describing the Task Parameters.


<h3 id="edit_email_configuration" title="Permalink">edit_email_configuration&nbsp;<a href="#edit_email_configuration" style="display: margin-left: 1em;">&para;</a></h3>

Configure email notification for the data map.

               Required Arguments:

               * `id` - The id of the data map.

               

<h3 id="export_canvas" title="Permalink">export_canvas&nbsp;<a href="#export_canvas" style="display: margin-left: 1em;">&para;</a></h3>

Generates an export JSON document all Canvas items.

This function is capable of exporting items from the "filesystem" repository, which is an administrative feature.

Optional Arguments:

* `project` - filter by a Canvas Project name.
* `component` - filter by a Canvas Component. (Project is required.)
* `repository` - specify the repository ('file' or 'db', 'db' if omitted.)

Returns: A JSON document containing Canvas items.


<h3 id="export_catalog" title="Permalink">export_catalog&nbsp;<a href="#export_catalog" style="display: margin-left: 1em;">&para;</a></h3>

Export all Project, Pipeline, Package, and Task definitions to a catalog as a JSON document.

Returns: A JSON document containing all Project, Pipeline, Package, and Task definitions.


<h3 id="export_package" title="Permalink">export_package&nbsp;<a href="#export_package" style="display: margin-left: 1em;">&para;</a></h3>

Export a Package Definition as a portable backup JSON document.

Required Arguments:

* `package` - the id or name of a Package.

Returns: A [Package Definition Object](api-response-objects#package-definition).


<h3 id="export_pipeline" title="Permalink">export_pipeline&nbsp;<a href="#export_pipeline" style="display: margin-left: 1em;">&para;</a></h3>

Export a Pipeline Definition as a portable backup JSON document.

Required Arguments:

* `pipeline` - the id or name of a Pipeline Definition.

Returns: A [Pipeline Definition Object](api-response-objects#pipeline-definition).


<h3 id="export_plugins" title="Permalink">export_plugins&nbsp;<a href="#export_plugins" style="display: margin-left: 1em;">&para;</a></h3>

None

<h3 id="export_progression" title="Permalink">export_progression&nbsp;<a href="#export_progression" style="display: margin-left: 1em;">&para;</a></h3>

Export a Progression Definition as a portable backup JSON document.

Required Arguments:

* `progression` - the id or name of a Progression.

Returns: A [Progression Definition Object](api-response-objects#progression-definition).


<h3 id="export_project" title="Permalink">export_project&nbsp;<a href="#export_project" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Project object for export.  (Will not include the `_id`.)

Required Arguments:

* `project` - the id or name of a Project.

Returns: A [Project Object](api-response-objects#project).


<h3 id="export_task" title="Permalink">export_task&nbsp;<a href="#export_task" style="display: margin-left: 1em;">&para;</a></h3>

Create a backup file for a single Task.

> The behavior of this command is different depending on the `Accept` header.

* If 'application/json' (default), it will return a JSON list of individual Task documents.
* If 'application/xml' OR 'text/plain', it will return an XML document of Tasks.

Required Arguments:

* `task` - Value can be either a Task ID, Code or Name.

Optional Arguments:

* `include_refs`` - If true, will analyze each task and include any referenced Tasks.

Returns: A collection of Task backup objects.


<h3 id="get_account" title="Permalink">get_account&nbsp;<a href="#get_account" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Cloud Account.

Required Arguments:

* `name` - a Cloud Account name or ID.

Returns: A [Cloud Account Object](api-response-objects#cloud-account).


<h3 id="get_asset" title="Permalink">get_asset&nbsp;<a href="#get_asset" style="display: margin-left: 1em;">&para;</a></h3>

Gets an Asset.

Required Arguments:

* `asset` - an Asset Name or ID.

Returns: An [Asset Object](api-response-objects#asset).


<h3 id="get_cloud" title="Permalink">get_cloud&nbsp;<a href="#get_cloud" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Cloud object.

Required Arguments: 

* `name` - a Cloud name or ID.

Returns: A [Cloud Object](api-response-objects#cloud).


<h3 id="get_data_map" title="Permalink">get_data_map&nbsp;<a href="#get_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Get list of data mappings.

If no 'mapping_id' is supplied, return all mappings.

Optional Arguments:

* `mapping_id` - data mapping to return

Returns: Result or error message.


<h3 id="get_feature_deliverycategory" title="Permalink">get_feature_deliverycategory&nbsp;<a href="#get_feature_deliverycategory" style="display: margin-left: 1em;">&para;</a></h3>

Get the `effective delivery category` for a feature, as determined by the condition of all that features workitems.

Required Arguments:

* `id` - The internal `_id` OR the authoritative `ID` from the origin system OR the `key` (user facing identifier) from the origin system.

Returns: An array of timeline events for the specified workitem.


<h3 id="get_license" title="Permalink">get_license&nbsp;<a href="#get_license" style="display: margin-left: 1em;">&para;</a></h3>

Get the license details.

Required Arguments:

* `license` - The text of a license key provided by Continuum.

Returns: The relevant properties of the current license.


<h3 id="get_log" title="Permalink">get_log&nbsp;<a href="#get_log" style="display: margin-left: 1em;">&para;</a></h3>

Gets the log for a specific service or automation instance.

Required Arguments:

* `process` - the name of the process of the log to retrieve.

Optional Arguments:

* `instance` - If process represents instanced data (such as pipelines or tasks), the `instance` is also required.
* `lines` - The number of log lines to retrieve.  (An integer, or the word `all`.  100 lines if omitted).
* `level` - Filter lines to a specific debug logging level _and higher_.  Default is all levels.  (Valid values: 10 (DEBUG), 20 (INFO), 30 (WARNING), 40 (ERROR), 50 (CRITICAL))
* `concatenate` - Concatenate log lines into a single text value.  Default is 'false' - returning an array of rows - if omitted. (Valid values: 'true' or 'false')

> NOTE: specifying `lines=all` can return a very large amount of data.

Returns: An array of log entries or a text buffer (depending on the `concatenate` option) in the requested format.


<h3 id="get_mappings_for_relationship" title="Permalink">get_mappings_for_relationship&nbsp;<a href="#get_mappings_for_relationship" style="display: margin-left: 1em;">&para;</a></h3>

Gets all the available data maps for given instances.

        Required Arguments:

        * `inbound_instance` - The system 1 instance id.
        * `outbound_instance` - The system 2 instance id.
        * `mappingId` - Id of current data map.

        Returns a list of data map objects.
        

<h3 id="get_next_id" title="Permalink">get_next_id&nbsp;<a href="#get_next_id" style="display: margin-left: 1em;">&para;</a></h3>

Get the next integer `id` in a named ID set.

Required Arguments:

* `name` - the name of the ID set

Optional Arguments:

* `reseed` - (integer) If provided, reset the pool to the specified value.  (This is the value that will be returned.)
* `fallback` - (integer) In the case of any errors, the provided `fallback` number will be returned. `0` if omitted.

Returns: 'true' on success, errors on failure.


<h3 id="get_package" title="Permalink">get_package&nbsp;<a href="#get_package" style="display: margin-left: 1em;">&para;</a></h3>

Returns the definition of the specified Package.

Required Arguments:

* `package` - Name of the Package.

Returns: The Package definition document.


<h3 id="get_package_manifest" title="Permalink">get_package_manifest&nbsp;<a href="#get_package_manifest" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="get_package_revision_manifest" title="Permalink">get_package_revision_manifest&nbsp;<a href="#get_package_revision_manifest" style="display: margin-left: 1em;">&para;</a></h3>

Returns the complete Manifest of a Package Version, given a range of Revisions.

Required Arguments:

* `package` - Name of the Package.
* `revision` - A specific Package Revision.

Optional Arguments:

* `verbose` - (`true`/`false`) Return verbose Manifest details.  `false` if omitted.

Returns: The Manifest (Workitems, Changes and Artifacts) of the specified Package Revision.


<h3 id="get_package_revision_phase_doc" title="Permalink">get_package_revision_phase_doc&nbsp;<a href="#get_package_revision_phase_doc" style="display: margin-left: 1em;">&para;</a></h3>

Creates a new Revision of a specified Version of a Package.

Required Arguments:

* `package` - Name of the Package.
* `revision` - A specific Package Revision.

Returns: Data about the current Revisions relationships in its Progression.


<h3 id="get_package_revision_progression" title="Permalink">get_package_revision_progression&nbsp;<a href="#get_package_revision_progression" style="display: margin-left: 1em;">&para;</a></h3>

Returns the Progression definition for a specific Package Revision.  (Name, Phase names and order, etc.)

Required Arguments:

* `package` - Name of the Package.
* `revision` - A specific Package Revision.

Returns: The Progression the specified Package Revision subscribes to.


<h3 id="get_pi_artifacts" title="Permalink">get_pi_artifacts&nbsp;<a href="#get_pi_artifacts" style="display: margin-left: 1em;">&para;</a></h3>

Gets the Changes from the Manifest of a Pipeline Instance.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Returns: A JSON document representing all Changes on the Manifest.

> Note: the response is 'json' - 'text' and 'xml' object_output options are not supported.


<h3 id="get_pi_changes" title="Permalink">get_pi_changes&nbsp;<a href="#get_pi_changes" style="display: margin-left: 1em;">&para;</a></h3>

Gets the Changes from the Manifest of a Pipeline Instance.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Returns: A JSON document representing all Changes on the Manifest.

Note: the response is 'json' - 'text' and 'xml' object_output options are not supported.


<h3 id="get_pi_data" title="Permalink">get_pi_data&nbsp;<a href="#get_pi_data" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Pipeline Instance Data object.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Optional Arguments:

* `lookup` - Lookup using an expression that evaluates to a subsection of the document.

Returns: A [Pipeline Instance](api-response-objects#pipeline-instance).

Note: the response is 'json' - 'text' and 'xml' object_output options are not supported.


<h3 id="get_pi_workitems" title="Permalink">get_pi_workitems&nbsp;<a href="#get_pi_workitems" style="display: margin-left: 1em;">&para;</a></h3>

Gets the Workitems from the Manifest of a Pipeline Instance.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Returns: A JSON document representing all Workitems on the Manifest.

Note: the response is 'json' - 'text' and 'xml' object_output options are not supported.


<h3 id="get_pipeline" title="Permalink">get_pipeline&nbsp;<a href="#get_pipeline" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Pipeline Definition object.

Required Arguments:

* `pipeline` - the id or name of a Pipeline Definition.

Returns: A [Pipeline Definition Object](api-response-objects#pipeline-definition).


<h3 id="get_pipelineinstance" title="Permalink">get_pipelineinstance&nbsp;<a href="#get_pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Pipeline Instance object.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.

Optional Arguments:

* `include_stages` - include Stage, Step and Plugin data and status.

Returns: A [Pipeline Instance](api-response-objects#pipeline-instance).


<h3 id="get_project" title="Permalink">get_project&nbsp;<a href="#get_project" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Project object.

Required Arguments:

* `project` - the id or name of a Project.

Returns: A [Project Object](api-response-objects#project).


<h3 id="get_project_changes" title="Permalink">get_project_changes&nbsp;<a href="#get_project_changes" style="display: margin-left: 1em;">&para;</a></h3>

Gets all the changes submitted to a Project.

Required Arguments:

* `project` - the id or name of a Project.

Returns: An array of change objects.


<h3 id="get_registry" title="Permalink">get_registry&nbsp;<a href="#get_registry" style="display: margin-left: 1em;">&para;</a></h3>

Gets a registry document by name.

Required Arguments:

* `name` - Name of the Registry document.

Returns: the entire Registry document on success, 'not found' otherwise.


<h3 id="get_settings" title="Permalink">get_settings&nbsp;<a href="#get_settings" style="display: margin-left: 1em;">&para;</a></h3>

Lists all the settings of modules.

Optional Arguments:

* `module` - name of the module. If omitted, all module settings are returned.

Returns: A [Settings Object](api-response-objects#settings).


<h3 id="get_submission" title="Permalink">get_submission&nbsp;<a href="#get_submission" style="display: margin-left: 1em;">&para;</a></h3>

Gets a raw 'Submission' payload using a query.

Required Arguments:

* `query` - Valid MongoDB query to identify the previous payload to resubmit.

> If the query would return multiple submissions, the newest one is matched.

Returns: the Submission document on success, 'not found' otherwise.


<h3 id="get_system_log" title="Permalink">get_system_log&nbsp;<a href="#get_system_log" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="get_task" title="Permalink">get_task&nbsp;<a href="#get_task" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Task object.

Required Arguments:

* `task` - Value can be either a Task ID or Name.

Optional Arguments:

* `include_code` - Whether to include Codeblocks and Steps.  (Only included if 'output_format' is 'json' or 'xml'.  'False' if omitted.)

Returns: A [Task Object](api-response-objects#task).


<h3 id="get_task_instance" title="Permalink">get_task_instance&nbsp;<a href="#get_task_instance" style="display: margin-left: 1em;">&para;</a></h3>

Gets the details of a Task Instance.

Required Arguments:
* `instance` - The Task Instance identifier.

Returns: A [Task Instance Object](api-response-objects#task-instance).


<h3 id="get_task_instance_status" title="Permalink">get_task_instance_status&nbsp;<a href="#get_task_instance_status" style="display: margin-left: 1em;">&para;</a></h3>

Gets just the Status of a Task Instance.

Required Arguments:

* `instance` - The Task Instance identifier.

Returns: The 'Status' from a [Task Instance Object](api-response-objects#task-instance).


<h3 id="get_task_instances" title="Permalink">get_task_instances&nbsp;<a href="#get_task_instances" style="display: margin-left: 1em;">&para;</a></h3>

Gets a list of Task Instances.

Optional Arguments:

* `filter` - A filter to limit the results.
* `status` - A comma separated list of statuses to filter the results.
* `from` - a date string to set as the "from" marker. (mm/dd/yyyy format)
* `to` - a date string to set as the "to" marker. (mm/dd/yyyy format)
* `records` - a maximum number of results to get.

Returns: A list of [Task Instance Objects](api-response-objects#task-instance).


<h3 id="get_task_log" title="Permalink">get_task_log&nbsp;<a href="#get_task_log" style="display: margin-left: 1em;">&para;</a></h3>

Gets the run log for a Task Instance.

Required Arguments:

* `instance` - The Task Instance identifier.

Returns: A [Task Log Object](api-response-objects#task-log).


<h3 id="get_task_parameters" title="Permalink">get_task_parameters&nbsp;<a href="#get_task_parameters" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Parameters template for a Task.

Required Arguments:

* `task` - Value can be either a Task ID, Code or Name.

Optional Arguments:

* `basic` - in JSON mode, if provided, will omit descriptive details.

Returns: An XML template defining the Parameters for a Task.

> This function is not affected by the output_format option.  The Response is always an XML document.



<h3 id="get_task_plans" title="Permalink">get_task_plans&nbsp;<a href="#get_task_plans" style="display: margin-left: 1em;">&para;</a></h3>

Gets a list of the queued execution plans for a Task.

Required Arguments:

* `task` - Value can be either a Task ID or Name.

Optional Arguments:

Returns: A list of [Execution Plan Objects](api-response-objects#execution-plan).


<h3 id="get_task_schedules" title="Permalink">get_task_schedules&nbsp;<a href="#get_task_schedules" style="display: margin-left: 1em;">&para;</a></h3>

Gets a list of Schedule definitions for a Task.

Required Arguments:

* `task` - Value can be either a Task ID or Name.

Optional Arguments:

Returns: A list of [Task Schedule Objects](api-response-objects#task-schedule).

* Text results do not include timing details.
* JSON results include Schedule definitions suitable for use in the 'schedule_task' function.


<h3 id="get_token" title="Permalink">get_token&nbsp;<a href="#get_token" style="display: margin-left: 1em;">&para;</a></h3>

Gets an authentication token for the API, which is the preferred alternative to 'Basic' authorization.

This function requires Basic authorization to be enabled.

Pass an `Authorization` header of type `Basic` to retrieve your Token.

If a token doesn't exist for the authenticated User, this method will generate a new token.

Returns: An authentication token.


<h3 id="get_transformer_assets" title="Permalink">get_transformer_assets&nbsp;<a href="#get_transformer_assets" style="display: margin-left: 1em;">&para;</a></h3>

Gets all asset types for the selected project in the selected transformer plugin instance.

        Required Arguments:

        * `plugin_id` - The id of the plugin.
        * `instance_id` - The id of the instance of the plugin.
        * `project_id` - The id of the selected project.

        Returns a list of the format {'id': <ASSET_ID>, 'name': <ASSET_NAME>}.
        

<h3 id="get_transformer_automap" title="Permalink">get_transformer_automap&nbsp;<a href="#get_transformer_automap" style="display: margin-left: 1em;">&para;</a></h3>

 Gets a data map for automapped fields

        Required Arguments:
        
        * `source_field_id` - The field id of the source system.
        * `target_field_id` - The field id of the target system.

        Returns a data map objct with automapped fields.
        

<h3 id="get_transformer_data_map" title="Permalink">get_transformer_data_map&nbsp;<a href="#get_transformer_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Gets a data map for listing.

        Required Arguments:

        * `id` - The id of the data map to be retrieved.

        Returns a single data map object.
        

<h3 id="get_transformer_data_map_all_sync_log" title="Permalink">get_transformer_data_map_all_sync_log&nbsp;<a href="#get_transformer_data_map_all_sync_log" style="display: margin-left: 1em;">&para;</a></h3>

None

<h3 id="get_transformer_data_map_sync_log_by_inbound" title="Permalink">get_transformer_data_map_sync_log_by_inbound&nbsp;<a href="#get_transformer_data_map_sync_log_by_inbound" style="display: margin-left: 1em;">&para;</a></h3>

None

<h3 id="get_transformer_data_maps" title="Permalink">get_transformer_data_maps&nbsp;<a href="#get_transformer_data_maps" style="display: margin-left: 1em;">&para;</a></h3>

Gets all the available data maps.

        Returns a list of data map objects.
        

<h3 id="get_transformer_datamap_for_edit" title="Permalink">get_transformer_datamap_for_edit&nbsp;<a href="#get_transformer_datamap_for_edit" style="display: margin-left: 1em;">&para;</a></h3>

Gets a data map for editing.

        Required Arguments:

        * `id` - The id of the data map to be retrieved.

        Returns a single data map object.
        

<h3 id="get_transformer_fields" title="Permalink">get_transformer_fields&nbsp;<a href="#get_transformer_fields" style="display: margin-left: 1em;">&para;</a></h3>

Gets all asset types for the selected project in the selected transformer plugin instance.

        Required Arguments:

        * `plugin_id` - The id of the plugin.
        * `instance_id` - The id of the instance of the plugin.
        * `project_id` - The id of the selected project.
        * `project_name` - The name of the selected project.

        Optional arguments:
        * `tracker_id` - The id of the selected tracker. (Mandatory for TF).
        * `tracker_name` - The name of the selected tracker. (Mandatory for TF).
        * `issuetype_id` - The id of the selected issyuetype. (Mandatory for Jira).
        * `issuetype_name` - The name of the selected issyuetype. (Mandatory for Jira).
        * `asset_type_id` - The id of the selected asset type. (Mandatory for V1).
        * `asset_type` - The name of the selected asset type. (Mandatory for V1).
        * `workitemtype_id` - The id of the selected workitem type. (Mandatory for Azure Devops).
        * `workitemtype_name` - The name of the selected workitem type. (Mandatory for Azure Devops).

        Returns a list of the format {'id': <ASSET_ID>, 'name': <ASSET_NAME>}.
        

<h3 id="get_transformer_fields_for_create" title="Permalink">get_transformer_fields_for_create&nbsp;<a href="#get_transformer_fields_for_create" style="display: margin-left: 1em;">&para;</a></h3>

Gets all asset types for the selected project for the 2 selected transformer plugin instances.

        Required Arguments:

        * `system_1` - Details of the first plugin instance.
        * `system_2` - Details of the second plugin instance.

        Mandatory Details for both system_1 and system_2.

        * `plugin_id` - The id of the plugin.
        * `instance_id` - The id of the instance of the plugin.
        * `asset` -
            * `project_id` - The id of the selected project.
            * `project_name` - The name of the selected project.

        Optional Details for both system_1 and system_2:
        * `asset` -
            * `tracker_id` - The id of the selected tracker. (Mandatory for TF).
            * `tracker_name` - The name of the selected tracker. (Mandatory for TF).
            * `issuetype_id` - The id of the selected issyuetype. (Mandatory for Jira).
            * `issuetype_name` - The name of the selected issyuetype. (Mandatory for Jira).
            * `asset_type_id` - The id of the selected asset type. (Mandatory for V1).
            * `asset_type` - The name of the selected asset type. (Mandatory for V1).

        Returns a list of the format {'id': <ASSET_ID>, 'name': <ASSET_NAME>}.
        

<h3 id="get_transformer_instances" title="Permalink">get_transformer_instances&nbsp;<a href="#get_transformer_instances" style="display: margin-left: 1em;">&para;</a></h3>

Gets all plugin instances that support transformer functionality.

        Returns a list of the following format.
        {'id': <PLUGIN_ID>, 'name': <PLUGIN_NAME>, 'instances': {'id': <INSTANCE_ID>, 'name': <INSTANCE_NAME>}
        

<h3 id="get_transformer_projects" title="Permalink">get_transformer_projects&nbsp;<a href="#get_transformer_projects" style="display: margin-left: 1em;">&para;</a></h3>

Gets all projects in the selected transformer plugin instance.

        Required Arguments:

        * `plugin_id` - The id of the plugin.
        * `instance_id` - The id of the instance of the plugin.

        Returns a list of the format {'id': <PROJECT_ID>, 'name': <PROJECT_NAME>}.
        

<h3 id="get_transformer_system_info_for_edit" title="Permalink">get_transformer_system_info_for_edit&nbsp;<a href="#get_transformer_system_info_for_edit" style="display: margin-left: 1em;">&para;</a></h3>

Gets a data map for listing without the field mapping info.

        Required Arguments:

        * `id` - The id of the data map to be retrieved.

        Returns a single data map object without field mapping info.
        

<h3 id="get_transformer_workflow" title="Permalink">get_transformer_workflow&nbsp;<a href="#get_transformer_workflow" style="display: margin-left: 1em;">&para;</a></h3>

Gets the workflow for given projects and asset type.

                Required Arguments:

                * `instance_id` - The system instance id.
                * `plugin_id` - The system plugin id.
                * `projects` - selected projects.
                *  `assets`  - selected asset

                Returns a workflow.
        

<h3 id="get_user_teams" title="Permalink">get_user_teams&nbsp;<a href="#get_user_teams" style="display: margin-left: 1em;">&para;</a></h3>

Get a list of all Teams of which the authenticated API user is a member, and their assigned Role.

Returns: A list of the User's Teams and Roles.


<h3 id="get_workitem" title="Permalink">get_workitem&nbsp;<a href="#get_workitem" style="display: margin-left: 1em;">&para;</a></h3>

Get the details of a specific workitem.

Required Arguments:

* `id` - The internal `_id` of the workitem OR the authoritative `ID` from the origin system OR the `key` (user facing identifier) from the origin system.

Returns: A workitem document.


<h3 id="get_workitem_deliverycategory" title="Permalink">get_workitem_deliverycategory&nbsp;<a href="#get_workitem_deliverycategory" style="display: margin-left: 1em;">&para;</a></h3>

Get all the packages a workitem is in, and the `effective delivery category` for the workitem.

Required Arguments:

* `id` - The internal `_id` of the workitem OR the authoritative `ID` from the origin system OR the `key` (user facing identifier) from the origin system.

Returns: An array of timeline events for the specified workitem.


<h3 id="get_workitem_parent" title="Permalink">get_workitem_parent&nbsp;<a href="#get_workitem_parent" style="display: margin-left: 1em;">&para;</a></h3>

Get the details of a specific feature.

Required Arguments:

* `id` - The internal `_id` of the feature OR the authoritative `ID` from the origin system OR the `key` (user facing identifier) from the origin system.

Returns: A workitem parent document.


<h3 id="get_workitem_timeline" title="Permalink">get_workitem_timeline&nbsp;<a href="#get_workitem_timeline" style="display: margin-left: 1em;">&para;</a></h3>

Get the timeline of a specific workitem.

Required Arguments:

* `id` - The internal `_id` of the workitem OR the authoritative `ID` from the origin system OR the `key` (user facing identifier) from the origin system.

Returns: An array of timeline events for the specified workitem.


<h3 id="get_worklist" title="Permalink">get_worklist&nbsp;<a href="#get_worklist" style="display: margin-left: 1em;">&para;</a></h3>

Gets a list of Pipeline in 'pending' status.

Optional Arguments:

* `filter` - a key:value filter to limit the results.

Returns: A list of pending Pipeline Instances.


<h3 id="healthcheck" title="Permalink">healthcheck&nbsp;<a href="#healthcheck" style="display: margin-left: 1em;">&para;</a></h3>

Performs a 'health check' on the sytem.

Returns: true/false if the system is 'healthy' and additional details.


<h3 id="import_backup" title="Permalink">import_backup&nbsp;<a href="#import_backup" style="display: margin-left: 1em;">&para;</a></h3>

Imports an XML or JSON backup file.

> DEPRECATED: this function is deprecated.  Use `import_task` instead.

Required Arguments:

* `import_text` - An XML or JSON document in the format of a Task backup file.

Returns: A list of items in the backup file, with the success/failure of each import.


<h3 id="import_catalog" title="Permalink">import_catalog&nbsp;<a href="#import_catalog" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="import_package" title="Permalink">import_package&nbsp;<a href="#import_package" style="display: margin-left: 1em;">&para;</a></h3>

Import a Package Definition from a backup file.

Required Arguments:

* `backup` - A JSON document formatted as a Package Definition backup.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

> If 'overwrite' is 'true' and the Definition exists, it will be replaced.

Returns: Success or error.


<h3 id="import_pipeline" title="Permalink">import_pipeline&nbsp;<a href="#import_pipeline" style="display: margin-left: 1em;">&para;</a></h3>

Import a Pipeline Definition.

Required Arguments:

* `backup` - A JSON document formatted as a complete Continuum Pipeline Definition backup.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

    If 'overwrite' is 'true' and the Definition exists, it will be replaced.

Returns: A [Pipeline Definition Object](api-response-objects#pipeline-definition).


<h3 id="import_progression" title="Permalink">import_progression&nbsp;<a href="#import_progression" style="display: margin-left: 1em;">&para;</a></h3>

Import a Progression Definition from a backup file.

Required Arguments:

* `backup` - A JSON document formatted as a Progression Definition backup.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

    If 'overwrite' is 'true' and the Progression exists, it will be replaced.

Returns: Success or error.


<h3 id="import_project" title="Permalink">import_project&nbsp;<a href="#import_project" style="display: margin-left: 1em;">&para;</a></h3>

Import a Project.

Required Arguments:

* `backup` - A JSON document formatted as a complete Project backup.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

    If 'overwrite' is 'true' the Project will be replaced.

Returns: A [Project Object](api-response-objects#project).


<h3 id="import_task" title="Permalink">import_task&nbsp;<a href="#import_task" style="display: margin-left: 1em;">&para;</a></h3>

Imports a Task backup file.

Required Arguments:

* `backup` - A JSON document in the format of a Task backup file.

Optional Arguments:

* `overwrite` - Valid values: true|false (default).

    If 'overwrite' is 'true' the Task(s) will be replaced.

> NOTE: There may be multiple Tasks in a single backup file, as often Tasks have dependencies on other Tasks, so all are included.

Returns: A list of items in the backup file, with the success/failure of each import.


<h3 id="initiate_pipeline" title="Permalink">initiate_pipeline&nbsp;<a href="#initiate_pipeline" style="display: margin-left: 1em;">&para;</a></h3>

Attempt to initiate a Pipeline Definition.

Required Arguments:

* `definition` - ID or Name of a Pipeline Definition to initiate.
* `project` - An identifying name for a Project. (ie: repo name)  Useful if a single pipeline definition supports multiple projects.
* `group` - Summary name, (ie: branch name) used to group all runs of this definition/project combination. Describes your 'use' of this Pipeline.

Optional Arguments:

* `instance_name` - An explicit name to use for this unique run.  (ie: commit id)
* `details` - a JSON object with additional properties for the Pipeline Instance, often required by specific plugins.

Returns: A [Pipeline Instance Object](api-response-objects#pipeline-instance).


<h3 id="install_add_on" title="Permalink">install_add_on&nbsp;<a href="#install_add_on" style="display: margin-left: 1em;">&para;</a></h3>

Installs an Add-On from the vs-exchange

Required Arguments:

* `name` - Name of the Add-On to install.

Optional Arguments:

* `team` - Team to which to add parts of the Add-On that are scoped to a team. Required if the Add-On contains any such parts.

Returns: `success` on success, errors otherwise.


<h3 id="install_license" title="Permalink">install_license&nbsp;<a href="#install_license" style="display: margin-left: 1em;">&para;</a></h3>

Installs a license file.

Required Arguments:

* `license` - The text of a license key provided by Continuum.

Returns: Success or Error message.


<h3 id="invoke_plugin" title="Permalink">invoke_plugin&nbsp;<a href="#invoke_plugin" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="list_add_ons" title="Permalink">list_add_ons&nbsp;<a href="#list_add_ons" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Add-Ons installed in this Continuum instance.

Optional Arguments:

* `include_contents` - If true, lists the names of all parts of each of the Add-Ons. Defaults to false

Returns: A list of Add-On details.


<h3 id="list_assets" title="Permalink">list_assets&nbsp;<a href="#list_assets" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Assets.

Optional Arguments:

* `filter` - will filter a value match on: (Multiple filter arguments can be provided, delimited by spaces.)

    * Asset Name
    * Port
    * Address
    * DB Name
    * Status
    * Credential Username

Returns: A list of [Asset Objects](api-response-objects#asset).


<h3 id="list_canvas_items" title="Permalink">list_canvas_items&nbsp;<a href="#list_canvas_items" style="display: margin-left: 1em;">&para;</a></h3>

Returns a list of all elements in the Canvas feature.

Optional Arguments:

* `project` - filter by a Canvas Project name.
* `component` - filter by a Canvas Component. (Project is required.)
* `repository` - specify the repository ('file' or 'db', 'db' if omitted.)

Returns: A list of all Canvas elements.


<h3 id="list_changes" title="Permalink">list_changes&nbsp;<a href="#list_changes" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Changes.

Optional Arguments:

* `project` - will limit the results to a specific 'project'.
* `group` - will limit the results to a specific 'group'.
* `since` - will only return changes since the provided timestamp.
* `managed` - will list only the managed changes.
* `unmanaged` - will list only the unmanaged changes.
* `limit` - will limit the number of changes.

Returns: A list of [Changes](restapi/api-response-objects.html#Changes){:target="robjs"}.


<h3 id="list_cloud_accounts" title="Permalink">list_cloud_accounts&nbsp;<a href="#list_cloud_accounts" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Cloud Accounts.

Optional Arguments: 

* `filter` - will filter a value match on:  (Multiple filter arguments can be provided, delimited by spaces.)

    * Account Name
    * Account Number
    * Provider
    * Login ID
    * Default Cloud Name

Returns: A list of [Cloud Account Objects](api-response-objects#cloud-account).


<h3 id="list_cloud_keypairs" title="Permalink">list_cloud_keypairs&nbsp;<a href="#list_cloud_keypairs" style="display: margin-left: 1em;">&para;</a></h3>

Lists all the Key Pairs defined on a Cloud.

Required Arguments:

* `cloud` - Name or ID of a Cloud.

Returns: A list of [Cloud KeyPair Objects](api-response-objects#cloud-keypair).


<h3 id="list_clouds" title="Permalink">list_clouds&nbsp;<a href="#list_clouds" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Clouds.

Optional Arguments: 

* `filter` - will filter a value match on:  (Multiple filter arguments can be provided, delimited by spaces.)

    * Cloud Name
    * Provider
    * Default Account Name
    * API URL

Returns: A list of [Cloud Objects](api-response-objects#cloud).


<h3 id="list_credentials" title="Permalink">list_credentials&nbsp;<a href="#list_credentials" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Shared Credentials.

Optional Arguments:

* `filter` - will filter a value match in Credential Name, Username, Domain or Description.  (Multiple filter arguments can be provided, delimited by spaces.)

Returns: A list of [Credential Objects](api-response-objects#credential).


<h3 id="list_packages" title="Permalink">list_packages&nbsp;<a href="#list_packages" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Package Definitions.

Returns: A list of [Package Definition Objects](api-response-objects#package-definition).


<h3 id="list_pipelinegroups" title="Permalink">list_pipelinegroups&nbsp;<a href="#list_pipelinegroups" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Pipeline Instance Groups (Stories).

Optional Arguments:

* `pipeline` - will limit the results a specific Pipeline Definition.
* `project` - will limit the results a specific 'project'.
* `group` - will limit the results to a specific 'group'.

Returns: A list of [Pipeline Instance Group Objects](api-response-objects#pipeline-instance-group).


<h3 id="list_pipelineinstances" title="Permalink">list_pipelineinstances&nbsp;<a href="#list_pipelineinstances" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Pipeline Instances.

Optional Arguments:

* `definition` - will limit the results a specific Pipeline Definition.
* `project` - will limit the results to a specific 'project'.
* `group` - will limit the results to a specific 'group'.
* `since` - Will only return instances since the provided timestamp.
* `limit` - Limit the number of results.  (0 for all results, 100 if omitted.)

Returns: A list of [Pipeline Instance Objects](api-response-objects#pipeline-instance).


<h3 id="list_pipelines" title="Permalink">list_pipelines&nbsp;<a href="#list_pipelines" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Pipeline Definitions.

Returns: A list of [Pipeline Definition Objects](api-response-objects#pipeline-definition).


<h3 id="list_processes" title="Permalink">list_processes&nbsp;<a href="#list_processes" style="display: margin-left: 1em;">&para;</a></h3>

Lists all running processes.

Returns: A list of [Process Objects](api-response-objects#process).


<h3 id="list_progressions" title="Permalink">list_progressions&nbsp;<a href="#list_progressions" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Progressions.

Returns: A list of [Progression Objects](api-response-objects#progression.


<h3 id="list_projects" title="Permalink">list_projects&nbsp;<a href="#list_projects" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Projects.

Optional Arguments:

Returns: A list of [Project Objects](api-response-objects#project).


<h3 id="list_registries" title="Permalink">list_registries&nbsp;<a href="#list_registries" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Registries

Returns: A list of [Registry Objects]


<h3 id="list_tags" title="Permalink">list_tags&nbsp;<a href="#list_tags" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Tags.

Optional Arguments:

* `filter` - will filter a value match in Tag Name.  (Multiple filter arguments can be provided, delimited by spaces.)

Returns: A list of [Tag Objects](api-response-objects#tag).


<h3 id="list_tasks" title="Permalink">list_tasks&nbsp;<a href="#list_tasks" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Tasks..

Optional Arguments:

* `filter` - will filter a value match in Task Name, Code or Description.  (Multiple filter arguments can be provided, delimited by spaces.)

Returns: A list of [Task Objects](api-response-objects#task).

> The Task Objects returned to this function are streamlined - they do not contain all the properties available in the `get_task` endpoint.


<h3 id="list_users" title="Permalink">list_users&nbsp;<a href="#list_users" style="display: margin-left: 1em;">&para;</a></h3>

Lists all registered Users.

Optional Arguments:

* `filter` - will filter a value match on: (Multiple filter arguments can be provided, delimited by spaces.)

    * Full Name
    * Login ID
    * Role
    * Email address

Returns: A list of [User Objects](api-response-objects#user).


<h3 id="metric" title="Permalink">metric&nbsp;<a href="#metric" style="display: margin-left: 1em;">&para;</a></h3>

Given a named metric and required context retrieve the value of that metric

    Required Arguments:

    * `type` - The name of the desired metric
    * `context` - A collection of key value pairs specific to the type provided

    Returns: The value of the the requested metric
    

<h3 id="new_revision" title="Permalink">new_revision&nbsp;<a href="#new_revision" style="display: margin-left: 1em;">&para;</a></h3>

Creates a new Revision of a specified Version of a Package.

Required Arguments:

* `package` - Name of the Package to revise.
* `version` - Version in which to create a new Revision.  (Package Revisions increment _within specific Versions_.)

Optional Arguments:

* `full_version` - Full Version of package to promote, optional alternative selector to `revision`.

> Note: Often, it is desireable that the `full_version` actually contain the number of the newly created Revision.
A special keyword, `__NEWREVISION`, is recognized in the value provided for `full_version` and will be replaced with the new Revision number.

Returns: A Package Revision document if successful, errors otherwise.


<h3 id="override_control" title="Permalink">override_control&nbsp;<a href="#override_control" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="post_pi_data" title="Permalink">post_pi_data&nbsp;<a href="#post_pi_data" style="display: margin-left: 1em;">&para;</a></h3>

Post data to the Workspace on a running Pipeline Instance.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.
* `key` - key to set in the Workspace data.
* `value` - value for the provided key.

All data is posted under a parent key - 'returns', to protect the overall Workspace.

Returns: 'true' on success, errors on failure.

Example using curl using a variable for the pipeline instance id and posting an array of values:

    curl -X POST -H "Content-Type: application/json" -H "Authorization: Token 5752fb9abb288013973fabf4" -d "{\"pi\": \"$PI_ID\", \"key\":\"hello\", \"value\": [\"world2\", \"earth\", \"mars\"]}" "http://continuum-server.example.com:8080/api/post_pi_data"



<h3 id="promote_revision" title="Permalink">promote_revision&nbsp;<a href="#promote_revision" style="display: margin-left: 1em;">&para;</a></h3>

Promotes a Package Revision to a particular Phase.

Required Arguments:

* `package` - Name of the Package to promote to a Progression Phase.
* `revision` - Revision number of a Package to promote, takes precedence over `full_version`.
* `full_version` - Optional Full Version of package to promote, optional alternative selector to `revision`.
* `phase` - Name of the Phase to which the specified Package Revision will be promoted.

Optional Arguments:

* `new_version` - If provided, all Revisions being promoted will be updated to the provided `new_version`.  (Will attempt to also update `full_version` if possible.)

Returns: `success` on success, errors otherwise.


<h3 id="register_artifact" title="Permalink">register_artifact&nbsp;<a href="#register_artifact" style="display: margin-left: 1em;">&para;</a></h3>

Record a new revision of a specific Artifact.

Required Arguments:

* `project` - Name or ID of the Project where this Artifact is defined.
* `name` - Name of the Artifact to revise.
* `branch` - Branch in the repository from which this artifact was built.
* `location` - Optional URL or path to where this Artifact can be found.
* `build_data` - Optional JSON object additional data about the build.

Returns: `success` on success, errors otherwise.


<h3 id="remove_object_tag" title="Permalink">remove_object_tag&nbsp;<a href="#remove_object_tag" style="display: margin-left: 1em;">&para;</a></h3>

Removes a Tag from an object.

Required Arguments:

* `tag` - The name of the Tag.
* `object_id` - The ID of the object.
* `object_type` - The numeric type of the object.

Returns: Success message if successful, error message on failure.


<h3 id="remove_team" title="Permalink">remove_team&nbsp;<a href="#remove_team" style="display: margin-left: 1em;">&para;</a></h3>

Remove an empty Team.

Only a 'System Administrator' can remove a team.  If the credentials used for this API call
are not a Syetem Administrator, the call will not succeed.

Required Arguments:

* `team` - Name or ID of the Team to change.



<h3 id="remove_team_user" title="Permalink">remove_team_user&nbsp;<a href="#remove_team_user" style="display: margin-left: 1em;">&para;</a></h3>

Remove a User from a Team.

Only a 'Team Administrator' can manage Team membership.  If the credentials used for this API call
are not a Team Administrator for the specified Team, the call will not succeed.

Required Arguments:

* `team` - Name or ID of the Team to change.
* `user` - Name or ID of the User to remove.

Optional Arguments:

* `default` - Users must be in at least one Team.  If the removal operation would leave this User Teamless, specify a new default Team Name for the User. Will attempt to use `Default` if omitted.

> NOTE: if a new Default Team is assigned, the User will be given the `User` role in the Default Team


<h3 id="rerun_pipelineinstance" title="Permalink">rerun_pipelineinstance&nbsp;<a href="#rerun_pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>

Rerun an Instance, using the saved 'initial data'.

This creates a new Instance exactly as the provided one was started.

Required Arguments:

* `pi` - The Name or ID of a Pipeline Instance.

Returns: A [Pipeline Instance Object](api-response-objects#pipeline-instance).
        

<h3 id="reset_password" title="Permalink">reset_password&nbsp;<a href="#reset_password" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="resubmit_change" title="Permalink">resubmit_change&nbsp;<a href="#resubmit_change" style="display: margin-left: 1em;">&para;</a></h3>

Resubmits a change 'Submission' payload to the specified Project.

Required Arguments:

* `query` - Valid MongoDB query to identify the previous payload to resubmit.

> If the query would return multiple submissions, the newest one is matched.

Returns: 'true' on success, errors on failure.


<h3 id="resubmit_task_instance" title="Permalink">resubmit_task_instance&nbsp;<a href="#resubmit_task_instance" style="display: margin-left: 1em;">&para;</a></h3>

Resubmits an Errored or Cancelled Task Instance.  Resubmit is *only* valid on Errored or Cancelled Task Instances.

Required Arguments:

* `instance` - The Task Instance identifier.

Returns: Returns: Nothing if successful, error messages on failure.


<h3 id="resync_transformer_event" title="Permalink">resync_transformer_event&nbsp;<a href="#resync_transformer_event" style="display: margin-left: 1em;">&para;</a></h3>

 Resync failed event

        Required Arguments:

        * `inbound_id` - The inbound id of the failed event
        

<h3 id="retry_pipelineinstance" title="Permalink">retry_pipelineinstance&nbsp;<a href="#retry_pipelineinstance" style="display: margin-left: 1em;">&para;</a></h3>

Attempt to retry a failed Pipeline Instance.  Simply restarts it again at Phase One.

CAUTION: The Workspace data is not cleared or reset.  Depending on the design of the Pipeline,
this may not succeed, or might produce unexpected results.

Required Arguments:

* `pi` - The Name or ID of a Pipeline Instance.

Returns: A [Pipeline Instance Object](api-response-objects#pipeline-instance).


<h3 id="reversion_packagerevision" title="Permalink">reversion_packagerevision&nbsp;<a href="#reversion_packagerevision" style="display: margin-left: 1em;">&para;</a></h3>

Changes the Version of the specified (and all matching previous) Package Revisions.

Required Arguments:

* `package` - Name of the Package to promote to a Progression Phase.
* `revision` - Revision number of a Package to promote, takes precedence over `full_version`.
* `full_version` - Optional Full Version of package to promote, optional alternative selector to `revision`.
* `new_version` - If provided, all Revisions being promoted will be updated to the provided `new_version`.  (Will attempt to also update `full_version` if possible.)

Returns: `success` on success, errors otherwise.


<h3 id="run_metric" title="Permalink">run_metric&nbsp;<a href="#run_metric" style="display: margin-left: 1em;">&para;</a></h3>

Runs a specific metric.

Required Arguments:

* `module` - Name of the metrics module that contains the metric function to run
* `metric` - Name of a function definition in the specified module

Optional Arguments:

* `args` - a JSON object of arguments the target metric may require

Returns: `success` on success, errors otherwise.


<h3 id="run_task" title="Permalink">run_task&nbsp;<a href="#run_task" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="save_email_configuration" title="Permalink">save_email_configuration&nbsp;<a href="#save_email_configuration" style="display: margin-left: 1em;">&para;</a></h3>

Configure email notification for the data map.

               Required Arguments:

               * `id` - The id of the data map.

               

<h3 id="schedule_tasks" title="Permalink">schedule_tasks&nbsp;<a href="#schedule_tasks" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="send_message" title="Permalink">send_message&nbsp;<a href="#send_message" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="set_pi_data" title="Permalink">set_pi_data&nbsp;<a href="#set_pi_data" style="display: margin-left: 1em;">&para;</a></h3>

Set Workspace data on a running Pipeline Instance.

Required Arguments:

* `pi` - the id or name of a Pipeline Instance.
* `key` - key to set in the Workspace data. (Certain internal keys are restricted and cannot be overridden.)
* `value` - value for the provided key.

> NOTE: USE WITH CAUTION! This function has the ability to overwrite values anywhere in
the Workspace.  For safer and more common cases, use 'post_pi_data'.

Returns: 'true' on success, errors on failure.

Example using curl:

    curl http://continuum-server.example.com:8080/api/set_pi_data?token=5752fb9abb288013973fabf4&key=hello&value=world&pi=57acb49a320c7a41bf32958a



<h3 id="set_pi_description" title="Permalink">set_pi_description&nbsp;<a href="#set_pi_description" style="display: margin-left: 1em;">&para;</a></h3>

Set the description of a specific Pipeline Instance

Required Arguments:

* `pi` - the id or name of a Pipeline Instance
* `description` - Description to set (HTML allowed)

Returns: 'true' on success, errors on failure.


<h3 id="set_pi_global_summary" title="Permalink">set_pi_global_summary&nbsp;<a href="#set_pi_global_summary" style="display: margin-left: 1em;">&para;</a></h3>

Set global summary data on a pipeline instance

Required Arguments:

* `pi` - the id or name of a pipeline instance
* `key` - key to set in the global summary
* `value` - value for the provided key

Returns: 'true' on success, errors on failure.

Example using curl:

    curl http://continuum-server.example.com:8080/api/set_pi_data?token=5752fb9abb288013973fabf4&key=hello&value=world&pi=57acb49a320c7a41bf32958a



<h3 id="set_pipelinegroup_number" title="Permalink">set_pipelinegroup_number&nbsp;<a href="#set_pipelinegroup_number" style="display: margin-left: 1em;">&para;</a></h3>

Set the autonumber root on Pipeline Instance Group. (Used to issue ascending numbers to Instances in the Group.)

Required Arguments:

* `pg` - The ID of a Pipeline Instance Group.
* `newnumber` - The new number to set as the autonumber root.

Returns: 'true' on success, errors on failure.


<h3 id="set_registry" title="Permalink">set_registry&nbsp;<a href="#set_registry" style="display: margin-left: 1em;">&para;</a></h3>

Sets values in a specific Registry document.

Required Arguments:

* `name` - Name of the Registry document.

Optional Arguments:

* `value` - Value to set at specified path, or entire document.  If omitted, target key or document will be cleared.
* `path` - If specified, will place `value` at this path.  If omitted, will update the entire document.
* `action` - Valid values: set | unset | addtoset | push | pull | merge
* `create` - Create named Registry if it doesn't exist? Valid values: true | false
* `options` - Additional Options. Dependent on the value of "action"
    * if `action: merge` is specified, the available options are:
        * `overwrite` - Overwrite exisiting keys on conflict? Valid values: true|false (default).
        * `deep` - Perform a shallow or deep merge when merging objects Valid values: true|false (default).

Returns: `success` on success, errors otherwise.


<h3 id="stop_task" title="Permalink">stop_task&nbsp;<a href="#stop_task" style="display: margin-left: 1em;">&para;</a></h3>

Stops a running Task Instance.

Required Arguments:

* `instance` - The Task Instance identifier.

Returns: Nothing if successful, error messages on failure.


<h3 id="submit_change" title="Permalink">submit_change&nbsp;<a href="#submit_change" style="display: margin-left: 1em;">&para;</a></h3>

Submits a change payload to the specified Project.

Required Arguments:

* `toproject` - the ID or Name of a Project.

> NOTE: This API is different than most others.  It's expecting a JSON
document as HTTP POST data.  The required `toproject` argument can either be
provided inside the POST data, or on the URL querystring.

Returns: 'true' on success, errors on failure.


<h3 id="test_plugin_connection" title="Permalink">test_plugin_connection&nbsp;<a href="#test_plugin_connection" style="display: margin-left: 1em;">&para;</a></h3>

Tests connectivity to a Plugin instance defined in the Continuum configuration.

Required Arguments:

One of:
* `plugin_name` - the name of a Plugin. (ex: v1plugin) This will look up the proper Module.
* `plugin` - DEPRECATED - the name of the Plugin PLUS the Module. (ex: v1plugin.main)

Optional Arguments:

* `instance` - A named Plugin instance in the Continuum configuration. If not used, the default instance will be tested.
* `team` - the Team to search for the Plugin Instance. Defaults to plugins available to All Teams.

Returns: A success message or error message


<h3 id="uninstall_add_on" title="Permalink">uninstall_add_on&nbsp;<a href="#uninstall_add_on" style="display: margin-left: 1em;">&para;</a></h3>

Uninstalls an Add-On from Continuum

Required Arguments:

* `name` - Name of the Add-On to uninstall.

Returns: `success` on success, errors otherwise.


<h3 id="update_cloud" title="Permalink">update_cloud&nbsp;<a href="#update_cloud" style="display: margin-left: 1em;">&para;</a></h3>

Updates a Cloud.

Required Arguments:
 
* `name` - Name or ID of the Cloud to update.

Optional Arguments:
 
* `apiurl` - URL of the Cloud API endpoint.
* `apiprotocol` - Cloud API endpoint protocol.
* `default_account` - the name of a default Account for this Cloud.

Returns: The updated [Cloud Object](api-response-objects#cloud).


<h3 id="update_settings" title="Permalink">update_settings&nbsp;<a href="#update_settings" style="display: margin-left: 1em;">&para;</a></h3>

Updates the settings of a process or module.

NOTE: the update_settings command requires submission of a JSON settings object.
As a guide for updating settings, first execute this command with the `Accept: application/json`
header (or output_format=json argument).

For example, to update Messenger settings, first do:

get_settings?module=messenger&output_format=json

...then use the result as a template for update_settings.

Required Arguments:

* `module` - name of the module to apply the settings.
* `settings` - a list of name:value setting objects.

Returns: Nothing if successful, error messages on failure.


<h3 id="update_transformer_data_map" title="Permalink">update_transformer_data_map&nbsp;<a href="#update_transformer_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Updates a data map.

        Required Arguments:

        * `id` - The id of the data map.

        Optional Arguments:

        * `name` - The name of the data map.
        * `direction_type` - The direction of the mapping (forward-direction, backward-direction or bi-direction).
        * `forward-direction` - The field mappings for the forward direction.
        * `backward-direction` - The field mappings for the backward direction.

        Returns the id of the data map.
        

<h3 id="update_transformer_data_map_with_new_fields" title="Permalink">update_transformer_data_map_with_new_fields&nbsp;<a href="#update_transformer_data_map_with_new_fields" style="display: margin-left: 1em;">&para;</a></h3>

Updates data map by fetching new fields from the target systems

        Required Arguments:
        *  id - The id of the data map


        Returns the id of the data map.
        

<h3 id="update_user" title="Permalink">update_user&nbsp;<a href="#update_user" style="display: margin-left: 1em;">&para;</a></h3>

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


<h3 id="v1_workitem_sync" title="Permalink">v1_workitem_sync&nbsp;<a href="#v1_workitem_sync" style="display: margin-left: 1em;">&para;</a></h3>

Accepts telemetry from Digital.ai Agility regarding changes to Workitems.

> NOTE: This API is specifically bound to the format of Digital.ai Agility webhooks.  It's expecting a JSON
document as HTTP POST data.  See the Digital.ai Agility webhooks documentation for the actual schema.

> This API hands processing off to a jobhandler thread.  Therefore it will always return 'success' in accepting the payload, or an error.
A 'success'ful API transaction does not mean that Continuum successfully processed the payload - watch the jobhandler log for details.


<h3 id="validate_instance" title="Permalink">validate_instance&nbsp;<a href="#validate_instance" style="display: margin-left: 1em;">&para;</a></h3>

Validate an instance of Continuum exists and the request is authenticated.

Returns: Success or Error message.


<h3 id="version" title="Permalink">version&nbsp;<a href="#version" style="display: margin-left: 1em;">&para;</a></h3>


Returns: The Continuum version.


# INTERNAL API FUNCTIONS

> The following endpoints are *for internal use*.  They are not guaranteed to remain in the API, and can change at any time without warning.  Use at your own risk.

<h3 id="associate_commits_to_v1_workitem" title="Permalink">associate_commits_to_v1_workitem&nbsp;<a href="#associate_commits_to_v1_workitem" style="display: margin-left: 1em;">&para;</a></h3>


Required Arguments:

* `commit_shas` - a list of all the Changes to associate to a Workitem.
* `associated_by` - User that made the association in Digital.ai Agility.
* `workitem_number` - Workitem number from Digital.ai Agility.
* `instance_url` - Digital.ai Agility instance url.


<h3 id="build_stream" title="Permalink">build_stream&nbsp;<a href="#build_stream" style="display: margin-left: 1em;">&para;</a></h3>


Gets all pipeline instances that a workitem participated in.

Required Arguments:

* `number` - a Workitem Identifier.

Returns: Related Pipeline Instances.


<h3 id="delete_workitems" title="Permalink">delete_workitems&nbsp;<a href="#delete_workitems" style="display: margin-left: 1em;">&para;</a></h3>


Permanently delete a matched set of Workitems.

> NOTE: This is a destructive operation that cannot be undone.  Deleting workitems affects audit history, package and automation manifests, and metrics.

Optional Arguments:

At least one of the following options must be provided.  These are matching criteria for the workitems to delete.

* `origin_project` - The Name or ID of the Project where the workitem originated.

Returns: 'true' on success, errors on failure.


<h3 id="winrm_command" title="Permalink">winrm_command&nbsp;<a href="#winrm_command" style="display: margin-left: 1em;">&para;</a></h3>


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


<h3 id="xlrelease_status" title="Permalink">xlrelease_status&nbsp;<a href="#xlrelease_status" style="display: margin-left: 1em;">&para;</a></h3>


This endpoint expects a customized response from XL Release.

This payload will be evaluated and mapped (if possible) to the appropriate Continuum context,
be that a Pipeline Instance, Package Revision, or other asset.

This payload must be an JSON object with the following two root level keys:

* `continuum_context` - All of the Continuum context that was passed to the XL Release when it was triggered.
* `xlrelease_details` - A document containing all the details of the XL Release - phases, tasks, status indicators, etc.

Example Payload:

```
{
    "continuum_context": {
        "project_id": "abc123",
        "pipeline_id": ""zyx890",
        "all the other": "data in the context"
    },
    "xlrelease_details": {
        "all the details": "of the release"
    }
}
```

Returns: HTTP Return Code, no data.

