MRI: Orthanc DICOM Server — Startup Guide
=====================================

.. Note::

   **MindCORE Neuroimaging Facility** | Last Updated: 21 July 2026

Overview
---------------

This document describes how to start and verify the Orthanc DICOM server
running on the MRI Research Center Mac Mini. Orthanc uses a PostgreSQL
database backend for the DICOM index, with DICOM files stored on the
connected G-RAID drive.

.. list-table:: System Architecture
   :widths: 40 60
   :header-rows: 1

   * - Component
     - Location
   * - Orthanc server
     - Mac Mini (mriuser)
   * - PostgreSQL database
     - Mac Mini internal drive
   * - DICOM file storage
     - /Volumes/G-RAID/Orthanc/OrthancStorage
   * - Web UI
     - http://localhost:8042
   * - DICOM port (AET: ORTHANC)
     - 4242

Before You Start — Preflight Checklist
---------------------------------------

Before launching Orthanc, verify the following:

1. **Logged in as mriuser** — PostgreSQL is registered as a LaunchAgent
   for this user and will only auto-start under this account.
2. **G-RAID drive is mounted** — Confirm ``/Volumes/G-RAID/`` is
   accessible in Finder or Terminal before starting Orthanc.
3. **PostgreSQL is running** — See verification steps below.

Step 1: Verify PostgreSQL is Running
--------------------------------------

PostgreSQL should start automatically when mriuser logs in.
To confirm, open Terminal and run:

.. code-block:: bash

   brew services list | grep postgresql

Expected output:

.. code-block:: text

   postgresql@16   started   mriuser   ~/Library/LaunchAgents/homebrew.mxcl.postgresql@16.plist

The status must show **started** and the user must show **mriuser**.

If PostgreSQL is stopped, start it manually:

.. code-block:: bash

   brew services start postgresql@16

If PostgreSQL shows an error status, check the log:

.. code-block:: bash

   cat /opt/homebrew/var/log/postgresql@16.log

Step 2: Verify the G-RAID is Mounted
--------------------------------------

.. code-block:: bash

   ls /Volumes/G-RAID/Orthanc/OrthancStorage

You should see Orthanc's hash-based folder structure. If the command
returns ``No such file or directory``, the RAID is not mounted — check
the physical connection and remount via Finder before proceeding.

Step 3: Start Orthanc
----------------------

Double-click **startOrthanc.command** in ``/Volumes/G-RAID/Orthanc`` in Finder, or run it from Terminal:

.. code-block:: bash

   /Volumes/G-RAID/Orthanc/startOrthanc.command

Orthanc will print startup messages to the terminal. Wait for this final
line before using the system:

.. code-block:: text

   Orthanc has started

Key lines to look for in the startup output:

.. list-table::
   :widths: 60 40
   :header-rows: 1

   * - Message
     - Meaning
   * - ``Using a custom database from plugins``
     - PostgreSQL index is active ✅
   * - ``Storage directory: /Volumes/G-RAID/...``
     - RAID storage is connected ✅
   * - ``DICOM server listening... on port: 4242``
     - Ready to receive DICOM data ✅
   * - ``HTTP server listening on port: 8042``
     - Web UI is available ✅
   * - ``Orthanc has started``
     - Fully ready ✅

Step 4: Access the Web Interface
----------------------------------

Open the Safari browser and navigate to:

.. code-block:: text

   http://localhost:8042

You should see the Orthanc Explorer 2 interface showing the DICOM database.

To confirm PostgreSQL is active as the database backend, navigate to:

.. code-block:: text

   http://localhost:8042/system

Look for ``"DatabaseBackendPlugin": "postgresql-index"`` in the JSON
response.

Step 5: Stopping Orthanc
--------------------------

Press **Ctrl+C** in the terminal window running ``startOrthanc.command``.

.. warning::

   Do not force-quit the terminal window without stopping Orthanc first
   — this can leave the database in an inconsistent state.

PostgreSQL does **not** need to be stopped manually — it will stop
automatically when mriuser logs out.

Troubleshooting
----------------

Orthanc fails to start — storage path not found
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The G-RAID is not mounted. Check the physical connection, wait for it
to mount in Finder, then try starting Orthanc again.

Orthanc fails to start — PostgreSQL connection error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PostgreSQL is not running. Start it with:

.. code-block:: bash

   brew services start postgresql@16

Then retry starting Orthanc.

Web UI not accessible at localhost:8042
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check that the ``startOrthanc.command`` terminal shows
``Orthanc has started``. If Orthanc is running but the UI is
unreachable, check for firewall settings blocking port 8042.

PostgreSQL shows error status in brew services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check the log file:

.. code-block:: bash

   cat /opt/homebrew/var/log/postgresql@16.log

Common causes:

- **Data directory ownership issue:**

  .. code-block:: bash

     sudo chown -R mriuser /opt/homebrew/var/postgresql@16

- **Port conflict:** Ensure no other PostgreSQL version is running
  (check for ``postgresql@14``).

Quick Reference
----------------

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Task
     - Command / URL
   * - Check PostgreSQL status
     - ``brew services list | grep postgresql``
   * - Start PostgreSQL manually
     - ``brew services start postgresql@16``
   * - Start Orthanc
     - ``./startOrthanc.command``
   * - Stop Orthanc
     - ``Ctrl+C`` in Orthanc terminal
   * - View Orthanc statistics
     - http://localhost:8042/statistics
   * - View system info
     - http://localhost:8042/system

System Details
---------------

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Setting
     - Value
   * - Orthanc version
     - 1.12.11
   * - PostgreSQL version
     - 16
   * - PostgreSQL database
     - orthancdb
   * - PostgreSQL port
     - 5432
   * - Orthanc HTTP port
     - 8042
   * - Orthanc DICOM port
     - 4242
   * - DICOM AET
     - ORTHANC
   * - Storage directory
     - /Volumes/G-RAID/Orthanc/OrthancStorage
   * - Config file
     - configMacOS.json

.. note::

   For further assistance, contact Dr. Kirwan via the MindCORE Neuroimaging Slack.