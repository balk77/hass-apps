Getting Started
===============

Installation on Hass.io
-----------------------

In order to use hass-apps in the hass.io ecosystem, you first need
to set up an AppDaemon add-on. The recommended add-on is `this one
<https://github.com/hassio-addons/addon-appdaemon3>`_.

Then, follow the steps for the `Installation in Docker <#id1>`_, because
that's what the add-on is build ontop of.


Installation in Docker
----------------------

1. When you have the official AppDaemon container up and running, create
   a file named ``requirements.txt`` in your ``apps`` directory (or one
   of its sub-directories) with one of the following contents. (Appdaemon `version 3.0.2 <https://appdaemon.readthedocs.io/en/3.0.2/HISTORY.html>`_ is required as a minimum)

   a) To always have the latest stable version of hass-apps installed
      when AppDaemon starts:

      ::

          hass-apps

   b) To install a specific version of hass-apps (e.g. v0.20181005.0):

   ::

       hass-apps==0.20181005.0

   c) To always have the latest development version installed (don't do
      this unless you know what you're doing):

   ::

       https://github.com/efficiosoft/hass-apps/archive/master.zip

3. Continue with the `configuration <#id2>`_ as normal.


Installation on GNU/Linux
-------------------------

Hass-apps is a collection of apps for `AppDaemon
<https://appdaemon.readthedocs.io/en/stable/>`_, hence AppDaemon is a
dependency of hass-apps and will automatically be installed alongside.

The project itself is developed on GNU/Linux, but since there are no
platform-specific Python modules used it should run everywhere Python
and AppDaemon are available. However, we'll assume an installation on
GNU/Linux for the rest of this guide. Feel free to apply it to your own
operating system.

The minimum required Python version is 3.5. To find out what you have
installed, run ``python3 --version``. If your version of Python is recent
enough, you may continue with installing.


Auto-Install Assistant
~~~~~~~~~~~~~~~~~~~~~~

There is a script available to guide you through the installation and
configuration. Just open a console, terminal, SSH session or whatever
and execute the following command. Execute it as the user that should
run AppDaemon later, doing this as root is strictly dissuaded from.

::

    wget -qO- https://raw.githubusercontent.com/efficiosoft/hass-apps/master/AIA.py > /tmp/AIA.py && python3 /tmp/AIA.py

Once the script has been downloaded, it'll run automatically. Follow
the instructions on screen.


Manual Installation
~~~~~~~~~~~~~~~~~~~

It is strongly recommended to install hass-apps (+ it's dependencies
like AppDaemon) into a virtualenv, separated even from Home Assistant in
order to avoid conflicts with different versions of dependency packages.

Other huge benefits of the virtualenv installation are that you neither
need root privileges nor do you pollute your system.with numerous tiny
packages that are complicated to remove, should you sometime wish to
do so.

The following simple steps will guide you through the installation
process.

1. If you use a distribution like Debian or Ubuntu which doesn't ship
   ``venv`` with Python by default, install it first. Whithout installing
   ``python3-venv``, you'd end up with a crippled virtualenv with pip,
   the Python package manager, not available. Of course you do need root
   privileges for this particular step.

   ::

       sudo apt install python3-venv

2. Then, create the virtualenv. We do this in a directory named
   ``appdaemon`` in this example inside the user's home directory.

   ::

        mkdir ~/appdaemon
       python3 -m venv ~/appdaemon/venv

3. Activate the virtualenv.

   ::

       cd ~/appdaemon
       source venv/bin/activate

4. Now install some common packages.

   ::

       pip install --upgrade pip setuptools wheel

5. And finally, install hass-apps.

   a) Install the latest stable version from PyPi (preferred).

      ::

          pip install --upgrade hass-apps

   b) Or, as an alternative, clone the Git repository to get even the
      latest changes. But please keep in mind that this shouldn't be
      considered stable and isn't guaranteed to work all the time. Don't
      use the development version in production unless you have a good
      reason to do so.

      ::

          git clone https://github.com/efficiosoft/hass-apps
          cd hass-apps
          pip install . --upgrade


Configuration
-------------

When you followed the above steps for installing hass-apps,
you automatically installed AppDaemon as well. Configuring
AppDaemon is out of the scope of this tutorial, but there
is a `Configuration Section in the AppDaemon Documentation
<https://appdaemon.readthedocs.io/en/stable/CONFIGURE.html>`_
which describes what to do. We assume that you've got a working AppDaemon
3.x for now.

1. Get yourself a nice cup of coffee or tea. You'll surely need it.
2. Store the file `hass_apps_loader.py
   <https://raw.githubusercontent.com/efficiosoft/hass-apps/master/hass_apps_loader.py>`_
   in your AppDaemon's ``apps`` directory. This is just a stub which
   imports the real app's code.
3. Pick one or more apps you want to use.
4. Copy the sample configuration provided for each app in the docs to a
   new YAML file in your AppDaemon's ``apps`` directory and start editing
   it. Adapt the sample configuration as necessary. Documentary comments
   explaining what the different settings mean are included.
   The sample configurations can also be found in the GitHub repository
   under ``docs/apps/<app_name>/sample-apps.yaml``.
5. AppDaemon should have noticed the changes made to ``apps.yaml`` and
   restart its apps automatically.

You're done, enjoy hass-apps!
