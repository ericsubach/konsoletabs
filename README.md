## KonsoleTabs ##

KonsoleTabs is a tool that allows you to open a Konsole window with named tabs, auto-executed commands within the tabs, and history -- all on a per-tab basis.

It is currently supports only bash and csh. It is trivial to add support for more shells.

### Configuration ###

KonsoleTabs uses a JSON-formatted configuration file to specify different profiles. A profile contains all the information pertaining to the tabs that should be opened. The default configuration file location is `~/.konsole_tabs`.

Each profile is required to have a name, the shell type, a history file, and tabs. Common commands and output redirection are optional. Within the tabs section, all fields are required except environment.

The ability to disable output redirection is offered due to problems I encountered with specific platforms.

The common commands, tab dir, commands, and environment values will expand the user path and environment variables.

#### Example ####

```json
[
{
   "profile": "sample",
   "shell": "bash",
   "history": "~/.bash_history",
   "redirect_output": "false",
   "common_commands": ["echo 'hi'"],
   "tabs":
   [
      {
         "name"    : "tab_1",
         "dir"     : "${FOO}/bar/",
         "history" : ["qmake", "make"],
         "commands": ["ls"],
         "environment":
         {
            "DEBUG_ENABLED" : "true"
         }
      },
      {
         "name"    : "tab_2",
         "dir"     : "~",
         "history" : [],
         "commands": ["find . -type f -name '*~' -delete"]
      }
   ]
}
]
```

### Usage ###

The program is invoked with the desired profile: `konsoletabs sample`

### Installation ###

There is no installation process, simply copy `konsoletabs` to a directory that is on your path

### Requirements ###

* Python 2.7
* The `pidof` program
* Recent enough Konsole version that uses D-Bus

### Limitations ###

* It was tested on the following platform and may work differently depending on the software versions:

      Qt: 4.8.6
      KDE Development Platform: 4.14.2
      Konsole: 2.14.2


* Tab names must not contain spaces
* Commands are executed blindly regardless of success
* It is currently restricted to creating a new window with tabs; it cannot alter a window that already exists
* There is always an extra tab left over from creating the initial session

