# Continuum REST API

## Response Objects

The Continuum REST API has many functions, most of which return CSK Objects, such as a Task.

The API supports three output formats - `text`, `json`, and `xml`.

API documentation will define what sort of object each function returns.  The defintions of those objects are listed below.

> Some API functions return a _*list*_ of object.  In this case, the output will be a JSON array of the object,
or an XML array, depending on the specified output format.

## Asset


### JSON

    {
        "Address": "",
        "Credentials": "",
        "ID": "",
        "Name": "",
        "SharedOrLocal": "",
        "Status": "",
        "Tags": []
    }

### XML

    <Asset>
        <Address />
        <Credentials />
        <ID />
        <Name />
        <SharedOrLocal />
        <Status />
        <Tags />
    </Asset>

### Text

The text response will include the following properties:

* Name
* Status
* Address
* SharedOrLocal
* Credentials


## Cloud


### JSON

    {
        "APIProtocol": "",
        "APIUrl": "",
        "DefaultAccount": "",
        "ID": "",
        "Name": "",
        "Provider": ""
    }

### XML

    <Cloud>
        <APIProtocol />
        <APIUrl />
        <DefaultAccount />
        <ID />
        <Name />
        <Provider />
    </Cloud>

### Text

The text response will include the following properties:

* ID
* Name
* Provider
* APIUrl
* APIProtocol
* DefaultAccount


## Cloud Account


### JSON

    {
        "AccountNumber": "",
        "DefaultCloud": "",
        "ID": "",
        "IsDefault": "",
        "LoginID": "",
        "Name": "",
        "Provider": ""
    }

### XML

    <CloudAccount>
        <AccountNumber />
        <DefaultCloud />
        <ID />
        <Name />
        <IsDefault />
        <LoginID />
        <Provider />
    </Cloud>

### Text

The text response will include the following properties:

* ID
* Name
* Provider
* AccountNumber
* LoginID
* DefaultCloud


## Cloud KeyPair


### JSON

    {
        "HasPassphrase": "",
        "HasPrivateKey": "",
        "ID": "",
        "Name": ""
    }

### XML

    <KeyPair>
        <HasPassphrase />
        <HasPrivateKey />
        <ID />
        <Name />
    </KeyPair>

### Text

The text response will include the following properties:

* Name


## Credential


### JSON

    {
        "Description": "",
        "Domain": "",
        "ID": "",
        "Name": "",
        "Type": "",
        "Username": ""
    }

### XML

    <Credential>
        <Description />
        <Domain />
        <ID />
        <Name />
        <Type />
        <Username />
    </Credential>

### Text

The text response will include the following properties:

* Name
* Username
* Domain
* Description


## Datastore Document


A Datastore Document is a document with a completely customizable schema.  Datastore Documents are stored in
MongoDB, therefore are JSON in their native format.

If the `xml` output format is specified, the API will make an attempt to convert the document to XML.

The `text` format makes no conversion attempt - `text` also returns a JSON representation.


## Execution Plan


### JSON

    {
        "ActionID": null,
        "PlanID": 0,
        "RunOn": "",
        "ScheduleID": "",
        "Source": ""
    }

### XML

    <Plan>
        <ActionID />
        <PlanID />
        <RunOn />
        <ScheduleID />
        <Source />
    </Plan>

### Text

The text response will include the following properties:

* PlanID
* RunOn
* Source
* ScheduleID


## Task


There are several ways a Task Object can be returned - basic and complete.  Some functions (that only need a list of Tasks)
will return the basic properties, and others will return the more complete object.

### JSON

#### Basic Response

    {
        "Code": "",
        "Description": "",
        "ID": "",
        "Name": "",
        "OriginalTaskID": "",
        "Status": "",
        "Tags": null,
        "Version": 1.0,
        "Versions": 1
    }

#### Additional Details in Complete Response

    {
        "ConcurrentInstances": "",
        "IsDefaultVersion": true,
        "NextMajorVersion": ",
        "NextMinorVersion": "",
        "NumberOfApprovedVersions": 0,
        "OriginalTaskID": "",
        "QueueDepth": ""
    }


### XML

    <Task>
        <Code />
        <ConcurrentInstances />
        <ID />
        <Description />
        <IsDefaultVersion />
        <Name />
        <NextMajorVersion />
        <NextMinorVersion />
        <NumberOfApprovedVersions />
        <OriginalTaskID />
        <QueueDepth />
        <Status />
        <Version />
    </Task>

### Text

The text response will include the following properties:

* Code
* Name
* Version
* Description
* Status
* IsDefaultVersion


## Task Instance


### JSON

    {
        "Instance": "",
        "account_id": "",
        "account_name": "",
        "allow_cancel": "",
        "asset_id": "",
        "asset_name": "",
        "ce_node": "",
        "cloud_id": "",
        "cloud_name": "",
        "completed_dt": "",
        "debug_level": 20,
        "options": {},
        "pid": "",
        "started_dt": "",
        "submitted_by": "",
        "submitted_by_instance": "",
        "submitted_dt": "",
        "summary": [],
        "task_id": "",
        "task_instance": "",
        "task_name": "",
        "task_name_label": "",
        "task_status": ""
    }

If a Task is doing work for another Continuum feature, the `options` property will contain additional useful information.

For example, in this case the Task Instance was doing work for a Pipeline Instance:

    "options": {
        "instance_id": "5c2f8f975d9e5d2ba5f516ce",
        "invoked_by": "pipeline_instance",
        "phase": "Build and Unit Test",
        "stage": "Build",
        "step": 15
    }


### XML

    <TaskInstance>
        <task_name_label />
        <pid />
        <debug_level />
        <account_name />
        <asset_id />
        <submitted_by />
        <cloud_id />
        <ce_node />
        <submitted_dt />
        <submitted_by_instance />
        <account_id />
        <completed_dt />
        <asset_name />
        <cloud_name />
        <task_instance />
        <task_id />
        <Instance />
        <started_dt />
        <allow_cancel />
        <task_name />
        <task_status />
        <options />
    </TaskInstance>

### Text

The text response will include the following properties:

* task_instance
* task_status
* task\_name\_label
* submitted_dt
* completed_dt


## Task Log


A Task Log will be a list of individual `log entry` items.  The complete Task Log contains additional information beyond the actual items.

### JSON

#### Task Log Object

    {
        "instance": "",
        "log_rows": [ "A list of 'log_row' Objects" ],
        "numrows": 0,
        "summary_rows": null,
        "task_id": "",
        "task_status": ""
    }

#### log_row Object

    {
            "codeblock_name": "",
            "command_text": "",
            "connection_name": "",
            "entered_dt": "",
            "function_label": "",
            "function_name": "",
            "log": "",
            "step_id": "",
            "step_order": 1,
            "task_id": "",
            "task_instance": 0,
            "variable_name": "",
            "variable_value": ""
        }

### XML

At this time, the XML response _does not_ contain additional details - it is simply an array of log_row Objects.

#### log_row Object

    <row>
        <codeblock_name />
        <command_text />
        <connection_name />
        <entered_dt />
        <function_label />
        <log />
        <step_id />
        <step_order />
        <task_id />
        <task_instance />
        <variable_name />
        <variable_value />
    </Process>


### Text

The text response will include the following properties:

* codeblock_name
* step_order
* function_name
* log


## Task Schedule


### JSON

    {
        "Days": [],
        "DaysOrWeekdays": "",
        "Debug": 50,
        "Description": "",
        "Hours": [],
        "Label": "",
        "Minutes": [],
        "Months": [],
        "Parameters": "",
        "ScheduleID": "",
        "Task": ""
    }

### XML

    <Schedule>
        <Days />
        <DaysOrWeekdays />
        <Debug />
        <Description />
        <Hours />
        <Label />
        <Minutes />
        <Months />
        <Parameters />
        <ScheduleID />
        <Task />
    </Schedule>

### Text

The text response will include the following properties:

* ScheduleID
* Label
* Description


## Pipeline Definition


### JSON

    {
        "_id": "",
        "name": "",
        "project": "",
        "description": "",
        "phases": []
    }

### XML

    <definition>
        <_id />
        <name />
        <project />
        <description />
        <phases />
    </definition>

### Text

The text response will include the following properties:

* _id
* name


## Phase


### JSON

    {
        "_id": "",
        "name": "",
        "description": "",
        "stages": []
    }

### XML

    <phase>
        <_id />
        <name />
        <description />
        <stages />
    </phase>

### Text

The text response will include the following properties:

* _id
* name


## Stage


### JSON

    {
        "_id": "",
        "name": "",
        "description": "",
        "ingate": {},
        "outgate": {},
        "steps": []
    }

### XML

    <stage>
        <_id />
        <name />
        <description />
        <ingate />
        <outgate />
        <steps />
    </stage>

### Text

The text response will include the following properties:

* _id
* name


## Project


### JSON

    {
        "_id": "",
        "name": ""
        "create_dt": "",
        "status": ""
    }

### XML

    <project>
        <_id />
        <name />
        <create_dt />
        <status />
    </stage>

### Text

The text response will include the following properties:

* _id
* name


## Pipeline Instance


### JSON

    {
        "_id": "",
        "name": "",
        "project": "",
        "pipeline_id": "",
        "pipeline_name": "",
        "pi_summary_id": "",
        "data": {},
        "phases": [],
        "start_dt": "",
        "end_dt": "",
        "status": ""
    }

### XML

    <pipelineinstance>
        <_id />
        <name />
        <project />
        <pipeline_id />
        <pipeline_name />
        <pi_summary_id />
        <data />
        <phases />
        <start_dt />
        <end_dt />
        <status />
     </pipelineinstance>

### Text

The text response will include the following properties:

* _id
* name


## Pipeline Instance Group


### JSON

    {
        "status": "", 
        "create_dt": "", 
        "project_id": "", 
        "group": "", 
        "project_team_id": "", 
        "project": "", 
        "pipeline_id": "", 
        "last_pi_number": 0, 
        "pipeline_name": "", 
        "pipeline_team_id": "", 
        "create_dt2": "", 
        "_id": ""
    }

### XML

    <pigroup>
        <status>
        <create_dt>
        <project_id>
        <group>
        <project_team_id>
        <project>
        <pipeline_id>
        <last_pi_number>
        <pipeline_name>
        <pipeline_team_id>
        <create_dt2>
        <_id />
    </pigroup>

### Text

The text response will include the following properties:

* _id
* name


## Settings


The Settings object is a complete description of the current Continuum system configuration.  `json` and `xml` will return the complete
configuration in the speficied output format.  `text` format is a special case, and it will format the settings into a readable format.

### Text

    Security
        AllowLogin : True
        PassMaxLength : 15
        PassMinLength : 6
        PasswordHistory : 0
        AutoLockReset : True
        PassComplexity : False
        PassMaxAttempts : 99
        PassRequireInitialChange : False

    Poller
        LoopDelay : 3
        Enabled : True


## User


> A User object contains secure information such as passwords.  This secure information is never included in a User object.

### JSON

    {
        "AuthenticationType": "",
        "Email": "",
        "FullName": "",
        "LastLoginDT": "",
        "LoginID": "",
        "Role": "",
        "Status": ""
    }

### XML

    <User>
        <AuthenticationType />
        <Email />
        <FullName />
        <LastLoginDT />
        <LoginID />
        <Role />
        <Status />
    </User>

### Text

The text response will include the following properties:

* FullName
* Role
* Status
* AuthenticationType
* Email


## Log Entry


To conserve space, log entries are stored with numeric codes for ObjectType.  Additionally, a log entry will have an `Action` and `LogType` property.

#### ObjectType:

    NA = 0
    User = 1
    Asset = 2
    Task = 3
    Schedule = 4
    Team = 5
    Tag = 7
    Image = 8
    MessageTemplate = 18
    Parameter = 34
    Credential = 35
    Domain = 36
    CloudAccount = 40
    Cloud = 41
    CloudKeyPair = 45
    CanvasItem = 50
    Pipeline = 60
    Phase = 61
    Stage = 62
    PipelineInstanceGroup = 63
    PipelineInstance = 64
    Project = 65
    ProjectArtifact = 66
    Package = 80
    PackageRevision = 81
    Progression = 90

#### LogTypes:

* Object
* Security
* Usage
* Other

#### Actions:

* UserLogin
* UserLogout
* UserLoginAttempt
* UserPasswordChange
* UserSessionDrop
* SystemLicenseException

* ObjectAdd
* ObjectModify
* ObjectDelete
* ObjectView
* ObjectCopy

* PageView
* ReportView

* APIInterface

* Other
* ConfigChange

### JSON

    {
        "Action": "",
        "Log": "",
        "LogDate": "",
        "LogType": "",
        "ObjectID": "",
        "ObjectType": 0,
        "User": ""
    }

### XML

    <item>
        <Action />
        <Log />
        <LogDate />
        <LogType />
        <ObjectID />
        <ObjectType />
        <User />
    </item>

### Text

The text response will include the following properties:

* User
* Action
* LogDate
* Log


## Process


### JSON

    {
        "Component": "",
        "Enabled": "",
        "Heartbeat": "",
        "Instance": "",
        "LoadValue": null,
        "MinutesIdle": 0,
        "hostname": "",
        "platform": ""
    }

### XML

    <Process>
        <Component />
        <Enabled />
        <Heartbeat />
        <Instance />
        <LoadValue />
        <MinutesIdle />
        <hostname />
        <platform />
    </Process>

### Text

The text response will include the following properties:

* Instance
* Component
* Heartbeat
* Enabled
* LoadValue
* MinutesIdle


## Tag


### JSON

    {
        "in_use": 5,
        "tag_desc": "Manage the Peoplesoft application.",
        "tag_name": "PeoplesoftAdmin"
    }

### XML

    <Tag>
        <in_use />
        <tag_desc />
        <tag_name />
    </Tag>

### Text

The text response will include the following properties:

* in_use
* tag_desc
* tag_name
