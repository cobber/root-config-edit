            ***** WARNING *****

THESE SCRIPTS WILL NOT WORK FOR FILES IN /boot!!!
The /config directory will probably NOT be available
at boot time - which would lead to broken sym-links!
config-edit has a check to prevent this.

            ***** WARNING *****

Author:      Stephen Riehm
Copyright:   2014-03-30
Last update: 2014-10-07

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
    /system
        OS only
        provides default configurations
        exact copy of installation image! (e.g. READ ONLY except during updates)
        must be able to run without configuration
        boot kernel etc. could also be stored here
            - no need for extra /boot partition since this partition should be read only anyway.
    /package
        additional package installations
        each package provides its own default configuration
        exact copy of package installation images! (e.g. READ ONLY except during updates)
        initial / automatic configuration should be confined to /Package/Configuration/<package name>
        it should be possible to maintain multiple versions of each package simultaneously
        it should be possible for users & programs to query the installed packages
        package source files etc. should NOT be stored here (use /data/source or /data/reference
    /host or /configuration
        ONLY contains MANUALLY configuration information
        list of installed packages
        configuration files for non-standard configurations
    /user, /data, /sites etc
        for everything else
