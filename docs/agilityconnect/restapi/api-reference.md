# Digital.ai Agility Connect REST API

<h3 id="cancel_transformer_event" title="Permalink">cancel_transformer_event&nbsp;<a href="#cancel_transformer_event" style="display: margin-left: 1em;">&para;</a></h3>

 Cancel failed event

        Required Arguments:

        * `inbound_id` - The inbound id of the failed event
        

<h3 id="check_transformer_data_map_name_exists" title="Permalink">check_transformer_data_map_name_exists&nbsp;<a href="#check_transformer_data_map_name_exists" style="display: margin-left: 1em;">&para;</a></h3>

Check if a mapping name already exists.

        Required Arguments:

        * `name` - The mapping name to be checked for existence.

        Returns a boolean indicating if the mapping already exists.
        

<h3 id="create_transformer_data_map" title="Permalink">create_transformer_data_map&nbsp;<a href="#create_transformer_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Creates a new data map.

        Required Arguments:

        * `name` - The name of the data map.
        * `direction_type` - The direction of the mapping (forward-direction, backward-direction or bi-direction).
        * `forward-direction` - The field mappings for the forward direction.
        * `backward-direction` - The field mappings for the backward direction.

        Returns the id of the newly created data map.
        

<h3 id="delete_transformer_data_map" title="Permalink">delete_transformer_data_map&nbsp;<a href="#delete_transformer_data_map" style="display: margin-left: 1em;">&para;</a></h3>

Delete the data map.

        Required Arguments:

        * `id` - The id of the data map.

        

<h3 id="edit_email_configuration" title="Permalink">edit_email_configuration&nbsp;<a href="#edit_email_configuration" style="display: margin-left: 1em;">&para;</a></h3>

Configure email notification for the data map.

               Required Arguments:

               * `id` - The id of the data map.

               

<h3 id="get_asset" title="Permalink">get_asset&nbsp;<a href="#get_asset" style="display: margin-left: 1em;">&para;</a></h3>

Gets an Asset.

Required Arguments:

* `asset` - an Asset Name or ID.

Returns: An [Asset Object](api-response-objects#asset).


<h3 id="get_license" title="Permalink">get_license&nbsp;<a href="#get_license" style="display: margin-left: 1em;">&para;</a></h3>

Get the license details.

Required Arguments:

* `license` - The text of a license key provided by Agility Connect.

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
        

<h3 id="get_project" title="Permalink">get_project&nbsp;<a href="#get_project" style="display: margin-left: 1em;">&para;</a></h3>

Gets a Project object.

Required Arguments:

* `project` - the id or name of a Project.

Returns: A [Project Object](api-response-objects#project).


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
        

<h3 id="get_workitem" title="Permalink">get_workitem&nbsp;<a href="#get_workitem" style="display: margin-left: 1em;">&para;</a></h3>

Get the details of a specific workitem.

Required Arguments:

* `id` - The internal `_id` of the workitem OR the authoritative `ID` from the origin system OR the `key` (user facing identifier) from the origin system.

Returns: A workitem document.


<h3 id="get_workitem_parent" title="Permalink">get_workitem_parent&nbsp;<a href="#get_workitem_parent" style="display: margin-left: 1em;">&para;</a></h3>

Get the details of a specific feature.

Required Arguments:

* `id` - The internal `_id` of the feature OR the authoritative `ID` from the origin system OR the `key` (user facing identifier) from the origin system.

Returns: A workitem parent document.


<h3 id="healthcheck" title="Permalink">healthcheck&nbsp;<a href="#healthcheck" style="display: margin-left: 1em;">&para;</a></h3>

Performs a 'health check' on the sytem.

Returns: true/false if the system is 'healthy' and additional details.


<h3 id="install_license" title="Permalink">install_license&nbsp;<a href="#install_license" style="display: margin-left: 1em;">&para;</a></h3>

Installs a license file.

Required Arguments:

* `license` - The text of a license key provided by Agility Connect.

Returns: Success or Error message.


<h3 id="list_projects" title="Permalink">list_projects&nbsp;<a href="#list_projects" style="display: margin-left: 1em;">&para;</a></h3>

Lists all Projects.

Optional Arguments:

Returns: A list of [Project Objects](api-response-objects#project).


<h3 id="list_users" title="Permalink">list_users&nbsp;<a href="#list_users" style="display: margin-left: 1em;">&para;</a></h3>

Lists all registered Users.

Optional Arguments:

* `filter` - will filter a value match on: (Multiple filter arguments can be provided, delimited by spaces.)

    * Full Name
    * Login ID
    * Role
    * Email address

Returns: A list of [User Objects](api-response-objects#user).


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


<h3 id="resync_transformer_event" title="Permalink">resync_transformer_event&nbsp;<a href="#resync_transformer_event" style="display: margin-left: 1em;">&para;</a></h3>

 Resync failed event

        Required Arguments:

        * `inbound_id` - The inbound id of the failed event
        

<h3 id="save_email_configuration" title="Permalink">save_email_configuration&nbsp;<a href="#save_email_configuration" style="display: margin-left: 1em;">&para;</a></h3>

Configure email notification for the data map.

               Required Arguments:

               * `id` - The id of the data map.

               

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
A 'success'ful API transaction does not mean that Agility Connect successfully processed the payload - watch the jobhandler log for details.


<h3 id="validate_instance" title="Permalink">validate_instance&nbsp;<a href="#validate_instance" style="display: margin-left: 1em;">&para;</a></h3>

Validate an instance of Agility Connect exists and the request is authenticated.

Returns: Success or Error message.


<h3 id="version" title="Permalink">version&nbsp;<a href="#version" style="display: margin-left: 1em;">&para;</a></h3>


Returns: The Agility Connect version.

