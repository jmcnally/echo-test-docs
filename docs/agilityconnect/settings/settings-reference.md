

## License

_Configuration section for managing the License Key._

#### License

_Enter the provided license key for this installation._



## Messenger

_The Messenger service is responsible for sending email notifications._

#### SMTP Connection Timeout

_Timeout (in seconds) to wait before giving up trying to connect._

* Data Type: `integer`


#### SMTP User Account

_User account for the SMTP server if authentication is required._



#### From Name

_The name any messages will appear 'From'_



#### Enabled

_Enable or Disable the Service._



#### Retry Delay

_Delay (in seconds) to wait before retrying a failed send._

* Data Type: `integer`


#### Retry Max Attempts

_Number of times to retry sending when errors are encountered before giving up._

* Data Type: `integer`


#### Administrative Emails

_A list of users who will receive system status and warning information._



#### From Email

_The email address any messages will appear 'From'_



#### SMTP User Password

_User password for the SMTP server if authentication is required._



#### SMTP Server Port

_Port number of the SMTP server._

* Data Type: `integer`


#### Use Legacy SSL

_Use legacy SSL connections. (uncommon)_



#### SMTP Server Address

_Address of the SMTP server._



## Poller

_The 'Automate Poller' is responsible for monitoring the queue and starting Automate Tasks._

#### Loop Delay

_Number of seconds to sleep between queue checks._

* Data Type: `integer`


#### Debug

_Set the debug level of the process. (10=DEBUG, 20=INFO, 30=WARNING, 40=ERROR, 50=CRITICAL)_



#### Enabled

_Enable or Disable the Service._



#### Server

_Agility Connect Server URL to which Poller/Task Engine will communicate._



## Security

_Security Policy and settings for the application._

#### Verbose Page View Logging

_Enable for debug/audit purposes. Writes a Security Log entry for every page access by every user._



#### Password Minimum Length

_Minumum allowed length for a valid password._

* Data Type: `integer`


#### New User Welcome Email

_The body of an email sent to new user accounts._



#### Password Maximum Age

_Maximum age a password will be allowed. Changing this setting will force a user to change their password immediately if their current password is older than the new Max age._

* Data Type: `integer`


#### Login Message

_A message to display on the Login page._



#### Password Age Warning Days

_Number of days before expiration to begin warning the user about password expiration._

* Data Type: `integer`


#### Password Maximum Length

_Maximum allowed length for a password._

* Data Type: `integer`


#### Authentication Error Message

_A customized message that appears when there are failed login attempts._



#### Password History

_The number of historical passwords to cache and prevent reuse._

* Data Type: `integer`


#### Auto Lock Reset

_The number of minutes before failed password lockout expires._

* Data Type: `integer`


#### Complex Password?

_Require 'complex' passwords? (numbers and special character)_



#### Password Maximum Attempts

_Maximum number of failed login attempts allowed before locking the account._

* Data Type: `integer`


## SSO

_Settings for the 'SSO' module._

#### Inbound Webhooks Debug

_Set the debug level of the processing of Inbound Webhooks. (10=DEBUG, 20=INFO, 30=WARNING, 40=ERROR, 50=CRITICAL)_

* Data Type: `integer`


## System

_Global system configuration items and other settings not specific to any other category._

#### MessageHub URL (External)

_Force all generated URLs to use the specified value._

* Config File Setting: `msghub_external_url`


#### LDAP/AD Port

_LDAP/AD service port_

* Data Type: `integer`
* Config File Setting: `ldap_port`


#### Core Service Debug

_Set the debug level of the process. (10=DEBUG, 20=INFO, 30=WARNING, 40=ERROR, 50=CRITICAL)_

* Data Type: `integer`
* Config File Setting: `core_debug`


#### MessageHub Bind Address

_Bind the Agility Connect MessageHub to a local address, overrides 0.0.0.0_

* Config File Setting: `msghub_bind_address`


#### UI SSL Key

_SSL Certificate to use for the UI._

* Config File Setting: `ui_ssl_key`


#### LDAP/AD Server

_LDAP/AD Server for User Authentication_

* Config File Setting: `ldap_server`


#### UI URL (External)

_Force all generated URLs to use the specified value._

* Config File Setting: `ui_external_url`


#### Canvas Temp Directory

_Canvas temporary directory for file uploads._

* Config File Setting: `dash_api_tmpdir`


#### MessageHub Port

_Run on the specified TCP port._

* Config File Setting: `msghub_port`


#### Message History

_Number of days of email message queue history to keep._

* Data Type: `integer`
* Config File Setting: `message_history`


#### Share Usage Statistics

_Share usage statistics with Digital.ai Agility?_

* Config File Setting: `usage_sharing`


#### Core Service Loop

_Loop timer for the Core service._

* Data Type: `integer`
* Config File Setting: `core_loop`


#### UI Debug

_Set the debug level of the process. (10=DEBUG, 20=INFO, 30=WARNING, 40=ERROR, 50=CRITICAL)_

* Data Type: `integer`
* Config File Setting: `ui_debug`


#### Agility Connect DataSync Debug

_Set the debug level of the process. (10=DEBUG, 20=INFO, 30=WARNING, 40=ERROR, 50=CRITICAL)_

* Data Type: `integer`
* Config File Setting: `echo_datasync_debug`


#### Rest API Allowed Origins

_Comma-separated list of origins allowed to access the API._

* Config File Setting: `rest_api_allowed_origins`


#### Enable External Downloads

_Allow browsers to request external resources to improve performance?_

* Config File Setting: `enable_external_downloads`


#### MessageHub Enabled



* Config File Setting: `msghub_enabled`


#### UI Menu Canvas

_One or more name:path; entries to Canvas resources. Appear as a 'Custom Pages' link in the Main UI right-side menu._

* Config File Setting: `ui_menu_canvas`


#### UI SSL

_Run the UI in secure (https) mode?_

* Config File Setting: `ui_use_ssl`


#### Service Logs History

_Number of days of services logs to keep._

* Data Type: `integer`
* Config File Setting: `service_logs_history`


#### Single Server Database Logging

_Centralized logging to the database is disabled when 'Single Server Mode' is true.  Setting this 'true' explicitly ENABLES database logging in a single-server configuration.  While there are benefits in log management, there is a small performance impact._

* Config File Setting: `single_server_mode_db_logging`


#### Default Time Zone

_Default time zone for all users (users can override this time zone in My Account)_

* Config File Setting: `default_time_zone`


#### MessageHub Debug

_Set the debug level of the process. (10=DEBUG, 20=INFO, 30=WARNING, 40=ERROR, 50=CRITICAL)_

* Data Type: `integer`
* Config File Setting: `msghub_debug`


#### UI Bind Address

_Bind the Agility Connect UI to a local address, overrides 0.0.0.0_

* Config File Setting: `ui_bind_address`


#### Canvas Allowed Origins

_Comma-separated list of origins allowed to access Canvas resources._

* Config File Setting: `dash_api_allowed_origins`


#### LDAP/AD SSL?

_Use SSL for the LDAP/AD connection?_

* Config File Setting: `ldap_ssl`


#### Single Server Mode

_All work will execute on the main server instead of one or more configured 'worker' servers._

* Config File Setting: `single_server_mode`


#### Core Service Enabled



* Config File Setting: `core_enabled`


#### JobHandler Debug

_Set the debug level of the process. (10=DEBUG, 20=INFO, 30=WARNING, 40=ERROR, 50=CRITICAL)_

* Data Type: `integer`
* Config File Setting: `jobhandler_debug`


#### Rest API Basic Authentication

_Allow 'basic' authentication to the Rest API._

* Config File Setting: `rest_api_enable_basicauth`


#### UI Token Authentication

_Allow user token authentication to the UI._

* Config File Setting: `ui_enable_tokenauth`


#### UI SSL Certificate

_SSL Certificate to use for the UI._

* Config File Setting: `ui_ssl_cert`

