<h3 id="ctm-describe-api" title="Permalink">ctm-describe-api&nbsp;<a href="#ctm-describe-api" style="display: margin-left: 1em;">&para;</a></h3>


Retrieves a list of all REST API methods and their documentation.

    OPTIONAL PARAMETERS
        -l,--listonly            List the methods without documentation.
**Examples**

_To print a full listing of all api commands with documentation_

    ctm-describe-api

_To print only the names with the api commands sorted_

    ctm-describe-api -l


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

<h3 id="ctm-get-license" title="Permalink">ctm-get-license&nbsp;<a href="#ctm-get-license" style="display: margin-left: 1em;">&para;</a></h3>


Prints the license information including expiration date

**Examples**

    ctm-get-license


#### Associated API: **get\_license**

Get the license details.

Required Arguments:

* `license` - The text of a license key provided by Agility Connect.

Returns: The relevant properties of the current license.

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

<h3 id="ctm-install-license" title="Permalink">ctm-install-license&nbsp;<a href="#ctm-install-license" style="display: margin-left: 1em;">&para;</a></h3>


Installs or updates the Agility Connect/Continuum license by importing a license file

    REQUIRED PARAMETERS
        -i,--inputfile           Path to a license.dat file.
**Examples**

    ctm-install-license -i "~/license.lic"


#### Associated API: **install\_license**

Installs a license file.

Required Arguments:

* `license` - The text of a license key provided by Agility Connect.

Returns: Success or Error message.

<h3 id="ctm-list-commands" title="Permalink">ctm-list-commands&nbsp;<a href="#ctm-list-commands" style="display: margin-left: 1em;">&para;</a></h3>

Lists all installed ctm-* commands.  Accepts no arguments.

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


Returns: The Agility Connect version.

