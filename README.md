======================
Clever Python bindings
======================

Installation
============

From PyPi:

    pip install clever

or

    easy_install clever

Or from source:

    python setup.py install


Usage
=============

To get started, add the following to your Python script:

    import clever
    clever.api_key = 'YOUR_API_KEY'

The `clever` module exposes classes corresponding to resources:

* District
* School
* Section
* Student
* Teacher
* Event

Each exposes a class method `all` that returns a list of all data in that resource that you have access to. Keyword arguments correspond to the same query parameters supported in the HTTP API:

    schools = clever.School.all() # gets information about all schools you have access to
    schools = clever.School.all(where=json.dumps({'name': 'Of Hard Knocks'}))
    schools = clever.School.all(sort='state', limit=1)

The `retrieve` class method takes in a Clever ID, and returns a specific resource. The object (or list of objects in the case of `all`) supports accessing properties using either dot notation or dictionary notation:

    demo_school = clever.School.retrieve("4fee004cca2e43cf27000001")
    assert demo_school.name == 'Clever Academy'
    assert demo_school['name'] == 'Clever Academy'

CLI
========

The library comes with a basic command-line interface:

    $ export CLEVER_API_KEY=DEMO_KEY
    $ clever districts all
    Running the equivalent of:
    --
    curl https://api.getclever.com/v1.1/districts -H "Authorization: Basic REVNT19LRVk="
    --
    Starting new HTTPS connection (1): api.getclever.com
    API request to https://api.getclever.com/v1.1/districts returned (response code, response body)     of (200, '{"data":[{"data":{"name":"Demo District","id":"4fd43cc56d11340000000005"},"uri":"/v1.1/districts/4fd43cc56d11340000000005"}],"links":[{"rel":"self","uri":"/v1.1/districts"}]}')
    Result (HTTP status code 200):
    --
    {"data":[{"data":{"name":"Demo District","id":"4fd43cc56d11340000000005"},"uri":"/v1.1/districts/4fd43cc56d11340000000005"}],"links":[{"rel":"self","uri":"/v1.1/districts"}]}
    --

Run `clever -h` to see a full list of commands.

Feedback
=============

Questions, feature requests, or feedback of any kind is always welcome! We're available at [support@getclever.com](mailto:support@getclever.com).