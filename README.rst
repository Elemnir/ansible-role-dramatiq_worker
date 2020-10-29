===============================
 Ansible Role: dramatiq_worker
===============================

An Ansible role for setting up a Dramatiq worker service.

----------------
 Role Variables
----------------

Key role variables are documented with their default values below. See ``defaults/main.yml`` for a full list.

::

    dramatiq_worker_path: "/var/lib/dramatiq_worker"

Path to where the generated virtual environment and broker script will be stored.

::

    dramatiq_worker_user: "user"

User which the worker service will run under.

::

    dramatiq_worker_broker_host: "localhost"

Hostname where the Redis server that will serve as the broker for getting tasks.

::

    dramatiq_worker_broker_password: ""

Password for the broker Redis server, if one is set.

::

    dramatiq_worker_listen_queues: ""

A string of comma-separated queue names to limit which sets of tasks the worker will listen for.

::

    dramatiq_worker_additional_packages: []

A list of package names to be installed into the worker's virtual environment in addition to the required packages.

::

    dramatiq_worker_actors: []

The list of Python functions to be imported and wrapped as Dramatiq Actors. Each element should be a dictionary containing the following keys. 

    * ``from`` - The dotted path to a package
    * ``callable`` - The callable within the package to import
    * ``extra_args`` - Optionally, any additional arguments to provide to the ``dramatiq.actor()`` call to create the Actor.


------------------
 Example Playbook
------------------

::

    ---
    - hosts: localhost
      vars:
        dramatiq_worker_additional_packages:
          - mypackage
        dramatiq_worker_actors:
          - from: mypackage
            callable: do_long_running_task
      roles:
        - dramatiq_worker
