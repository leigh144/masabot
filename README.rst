MasaBot
=======
An automated discord bot for handling typical tasks.

Dev Setup
---------
Masabot requires python 3. If you don't have it, install it.

To install `masabot`, first clone the repo to the local system::

    git clone git@github.com:moe-serifu-circle/masabot.git

Masabot is currently a long-running foreground process; to prevent accidental disconnection it is highly-recommended
that it be executed in a terminal multiplexer such as ``screen`` in production environments. This is not required for
testing/dev set up.

Masabot has a ``setup.py``, which can be used to install all library dependencies, but this should be done in a virtual
environment. Set up one somewhere; this one uses masabot's home directory, and creates it in a directory that is ignored
by git::

    cd masabot
    python3 -m venv .venv

Then, to enter the virtual environment (which should always be done to avoid polluting the global python namespace), you
run the activation script.

On Windows, this is::

    .venv\Scripts\activate.bat

On Mac/Unix/Linux, this is::

    . .venv/bin/activate

The MasaBot start script will automatically search for and enter the virtual environment, so there is no need to be in
it when starting MasaBot. To exit the environment, execute the deactivation script::

    deactivate

Now the environment is prepared, but before launching masabot, its Configuration_ must be set up. Copy the
``config-example.json`` file to ``config.json``, and fill in the values approriately. At minimum, the
``discord-api-key`` must be set to the token for your bot, and the ``masters`` list should contain at least one user's
uuid. For information on obtaining a bot token, see `Obtaining a Discord Key`_ in the `Discord Integration`_ section;
for information on master users, see `Masters List`_ in the Configuration_ section.

Once `masabot` is fully configured, it can be started via its supervisor. To launch the masabot supervisor, execute the
`run-masabot.sh` script::

    ./run-masabot.sh

Assuming everything is configured properly, MasaBot will now be started and running on the servers she has been invited
to. You should see something like this::

    Logged in as MasaBotTestRun
    ID: 506801838553825281
    Avatar not yet set; uploading...
    Connected to servers:
    Bot is now online


animelist Module: Additional Setup
..................................

Anilist
~~~~~~~
First, go to anilist at  https://anilist.co/settings/developer and create a new API v2 client. Set the name to anything
you want, but be sure to set the redirect URI to something on your system.

Then, copy the secret and client ID to your ``config.json`` file.


Discord Integration
-------------------
In order to properly set up a bot, it will have to be set up to work with Discord. The instructions in this section will
take you through setting up a Discord application,


Environment Variables
---------------------
Some environment variables may be used to override settings in the ``config.json`` file. If present, the value
of the environment variable takes precedence over any that are defined in config.

The following environment variables are recognized:

* ``MASABOT_DISCORD_API_KEY`` corresponds to ``"discord-api-key"`` in the config file.

* ``MASABOT_ANIMELIST__ANILIST_CLIENT_ID`` corresponds to ``"animelist"."anilist-client-id"`` in the config file.

* ``MASABOT_ANIMELIST__ANILIST_CLIENT_SECRET`` corresponds to ``"animelist"."anilist-client-secret"`` in the config
  file.

* ``MASABOT_ANNOUNCE_CHANNELS`` corresponds to ``"announce-channels"`` in the config file. This variable contains the
  name of each room to announce in, separated by commas.


Integration Tests
-----------------
To execute integration tests, go to the project root directory and then type in `./run-int-tests.sh`.
