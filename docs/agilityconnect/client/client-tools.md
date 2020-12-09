# Agility Connect CLI

Digital.ai Agility Connect comes with a complete CLI (command line interface) that provides shell level access to the Digital.ai Agility Connect REST API. The CLI can be installed on any machine with network access to a Agility Connect environment.

## Installing the Tools

The CLI is written in the Python programming language and uses some Python tools to install. The instructions are slightly different whether on Linux / OSX or on Windows.

### Linux / OSX Install

To install the CLI on Linux or Mac OSX, you must first make sure you have Python 2.7 installed as well as the `pip` installer.

At the command line, run the following command:

    python -V

If python is not installed on your target machine, first install that. See https://www.python.org/downloads/. Make sure to choose the latest Python 2.7.x

Next run the following:

    pip -V

> If you have Python 2.7.9+ installed, `pip` should be installed as well. If not, see the following link: https://pip.pypa.io/en/latest/installing.html for installation instructions.

Once `python` and `pip` are ready, run the following command to install the CLI.

    pip install https://s3.amazonaws.com/downloads.continuum.versionone.com/continuum-client-latest.tar.gz

> If you receive an error running the command above, you may need to run the pip install command under `sudo`.

The commands should automatically be added to the user's path.

### Windows Install

To install the CLI on Windows, you also need to make sure you have Python 2.7 and `pip` installed.

First a command line session on Windows. Run the following command:

    python -V

Unlike Linux and Mac OSX, Python is not part of the standard Windows install so it is likely that the python command will not be found.  If Python is not installed on your target machine, first install that. See https://www.python.org/downloads/. Make sure to choose the latest Python 2.7.x.

> Make sure to allow the Python installer to associate `.py` file extensions with Python. *This is very important.*

Next run the following:

    pip -V

If `pip` is not available, see https://pip.pypa.io/en/latest/installing.html for installation instructions.

Now install the latest CLI for Windows.

    pip install https://s3.amazonaws.com/downloads.continuum.versionone.com/continuum-client-win-latest.tar.gz

The commands should automatically be added to the user's path.

> On Windows the all commands end with the `.py` file extension. This is because Windows uses the file extension to determine how the file should behave when executed. The Python installer will register itself as associated with the .py file. Anytime in the Digital.ai Agility Connect documentation that you see a CLI command referenced in an instruction, for Windows clients append the `.py` file extension on the command before running.


## Command Line Tools Usage

### Naming

All commands start with a `ctm-` prefix, to separate them from any other commands that may be in your PATH.

## Required Configuration

The CLI requires two important configuration values - a valid Agility Connect `URL` and `TOKEN`.  These two important values can be provided in several different ways.

### Persistent Configuration File

Most commmonly, you should set up a persistent *configuration file* on your environment.

Create a `.ctmclient.conf` file, typically in your $HOME directory.  Edit the file as follows:

    {
        "url": "http://serveraddress:8080",
        "token": "enter_token_here"
    }

Where `url` is the full URL of the Digital.ai Agility Connect server, and `token` is the string of characters you copied from your user profile in Agility Connect. Save the file.

Now test the commands ability to connect to the address and that the credentials are valid:

    ctm-version

Or on Windows

    ctm-version.py

The command should respond with a version number like `19.0.0.500`. If not, reconcile any error messages that were returned.

### Passing Credentials via Command Line

If you choose not to use a persistent configuration file, you can pass in the url and token as arguments to the commands.

    ctm-version --url http://localhost:8080 --token enter_token_here

> As an additional option, `--config foo.conf`, allows you to specify a different json configuration file other than `.ctmclient.conf` in the user's home directory. This allows you to save your details, if desired, in a different directory or file.

Any arguments passed on the command line take precedence over values stored in config files.

### ENVIRONMENT VARIABLES

Finally, you can set two specific environment variables - `CONTINUUM_URL` and `CONTINUUM_TOKEN`.

    export CONTINUUM_URL=http://localhost:8088
    export CONTINUUM_TOKEN=abc123zyx789

> Regarding *precedence*: As there are three different methods of providing configuration, the order of precedence is `ENVIRONMENT VARIABLES > args > file`

## Standard Arguments

All commands accept the following common arguments:

        -U,--url                 URL of the REST API endpoint. For example: http://address:port
        -T,--token               A valid users API token.
        -C,--config              Read token and url from the specified json formatted config file.
        -F,--format              The output format.  (default=text) Valid Values: text|json|xml
        -L,--output_delimiter    Delimiter for "text" output format. (default=TAB)
        -D,--debug               Turn on debugging output.
        -H,--help                Display this help message.
        --force                  Force "yes" on "Are you sure?" prompts.
        --noheader               For "text" output format, omit the column header.
        --dumpdoc                Writes documentation for the command in Markdown format.
        --api                    Identifies the API endpoint associated with this command.

### Command Specific Arguments

To see the specific arguments per command line tool, use the `--help` option as follows.

    ctm-list-tasks --help

### Full Command Listing and Help

See the [CLI Reference](command-reference) for a full listing of the commands available and their usage.


## Troubleshooting

If you are unsure of the configuration being used by the tools, use the `--debug` flag.  For example:

    ctm-version --debug

    Using CONTINUUM_URL: http://localhost:8088/api
    Using CONTINUUM_TOKEN: xxxx
    Trying an HTTP GET to http://localhost:8088/api/version
    ...
    Exception: ('API connection error. Check http or https, server address and port.')

> In this above example, the URL/port is not accessible.
