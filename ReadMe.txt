            ***** WARNING *****

DO NOT USE THESE SCRIPTS TO EDIT FILES IN /boot!!!
The /hosts directory will probably NOT be available
at boot time - which would lead to broken sym-links!

            ***** WARNING *****

MOTIVATION:

    Typically, a unix system is configured by editing text files in /etc and
    /usr/local/etc. These directories not only contain the files which were
    edited by the administrator, but they also contains all kinds of other
    files - most of which are never seen by the administrator.
    By relocating the files which were actually edited, the administrator can:
        quickly see what has been done in the past
        replicate the configuration simply
        revert to previous versions of configuration files (via git)
    Also, linked files can then be edited with any normal text editor, although
    this is not recommended, as the changes will not be checked into git
    automatically.

    maintainability:
        updates are simple - just overwrite
        possible to have multiple OS's installed and switch between them via /System link
        no interference between installed packages and OS
    easy to administer:
        look in /Host or /Configuration
        list of installed packages
        set of configuration files WHICH WERE ACTUALLY CREATED / EDITED to make the machine work
        should also include user information, networking, etc
        ideal place to put puppet stuff

My dream OS:
    /System
        OS only
        provides default configurations
        exact copy of installation image! (e.g. READ ONLY except during updates)
        must be able to run without configuration
    /Library
        additional package installations
        each package provides default configuration
        exact copy of package installation images! (e.g. READ ONLY except during updates)
        initial / automatic configuration should be confined to /Library/Configuration
    /Host or /Configuration
        ONLY contains MANUALLY configuration information
        list of installed packages
        configuration files for non-standard configurations
    /User, /Data, /Sites etc
        for everything else

