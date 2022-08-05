.. SPDX-License-Identifier: AGPL-3.0-or-later

----

.. figure:: https://raw.githubusercontent.com/searxng/searxng/master/src/brand/searxng.svg
   :target: https://docs.searxng.org/
   :alt: SearXNG
   :width: 100%
   :align: center

----

Set up guide: 
Based on default set up steps:
https://docs.searxng.org/admin/installation-searxng.html
(the only difference is the clone step, eg. 3.b)

These steps were performed on Ubuntu 20.04


1. Install packages:

a. $ sudo -H apt-get install -y \
    python3-dev python3-babel python3-venv \
    uwsgi uwsgi-plugin-python3 \
    git build-essential libxslt-dev zlib1g-dev libffi-dev libssl-dev



2. Create User:

a. $ sudo -H useradd --shell /bin/bash --system \
    --home-dir "/usr/local/searxng" \
    --comment 'Privacy-respecting metasearch engine' \
    searxng
	
b. $ sudo -H mkdir "/usr/local/searxng"

c. $ sudo -H chown -R "searxng:searxng" "/usr/local/searxng"



3. Install SearXNG

a. $ sudo -H -u searxng -i

b. (searxng)$ git clone "https://github.com/cofebe/searx.git" \
                   "/usr/local/searxng/searxng-src"

c. (searxng)$ python3 -m venv "/usr/local/searxng/searx-pyenv"

d. (searxng)$ echo ". /usr/local/searxng/searx-pyenv/bin/activate" \
                   >>  "/usr/local/searxng/.profile
				   

4. Install SearXNG Dependencies

a. exit the SearXNG bash session you opened above and start a new one

b. $ sudo -H -u searxng -i

c. (searxng)$ command -v python && python --version

#you should see
/usr/local/searxng/searx-pyenv/bin/python
Python 3.8.10

d. (searxng)$ pip install -U pip
e. (searxng)$ pip install -U setuptools
f. (searxng)$ pip install -U wheel
g. (searxng)$ pip install -U pyyaml

h. (searxng)$ cd "/usr/local/searxng/searxng-src"
i. (searxng)$ pip install -e .



5. Configuration:

a. Open a second terminal for the configuration tasks and leave the (searx)$ terminal open for step 6

b. $ sudo -H mkdir -p "/etc/searxng

c. $ sudo -H cp "/usr/local/searxng/searxng-src/utils/templates/etc/searxng/settings.yml" \
             "/etc/searxng/settings.yml"

c. edit /etc/searxng/settings.yml and replace "ultrasecretkey" with a password of your choosing.
	eg: $ sudo vim /etc/searxng/settings.yml



6. Launch App:

a. return to previous terminal, or open a new one and follow steps a.1-a.2
a.1 $ sudo -H -u searxng -i
a.2 (searxng)$ cd /usr/local/searxng/searxng-src

b. (searxng)$ export SEARXNG_SETTINGS_PATH="/etc/searxng/settings.yml"

c. (searxng)$ python searx/webapp.py

d. open a browser and navigate to http://127.0.0.1:8888

e. celebrate






Privacy-respecting, hackable `metasearch engine`_

If you are looking for running instances, ready to use, then visit searx.space_.
Otherwise jump to the user_, admin_ and developer_ handbooks you will find on
our homepage_.

|SearXNG install|
|SearXNG homepage|
|SearXNG wiki|
|AGPL License|
|Issues|
|commits|
|weblate|
|SearXNG logo|

----

.. _searx.space: https://searx.space
.. _user: https://docs.searxng.org/user
.. _admin: https://docs.searxng.org/admin
.. _developer: https://docs.searxng.org/dev
.. _homepage: https://docs.searxng.org/
.. _metasearch engine: https://en.wikipedia.org/wiki/Metasearch_engine

.. |SearXNG logo| image:: https://raw.githubusercontent.com/searxng/searxng/master/src/brand/searxng-wordmark.svg
   :target: https://docs.searxng.org/
   :width: 5%

.. |SearXNG install| image:: https://img.shields.io/badge/-install-blue
   :target: https://docs.searxng.org/admin/installation.html

.. |SearXNG homepage| image:: https://img.shields.io/badge/-homepage-blue
   :target: https://docs.searxng.org/

.. |SearXNG wiki| image:: https://img.shields.io/badge/-wiki-blue
   :target: https://github.com/searxng/searxng/wiki

.. |AGPL License|  image:: https://img.shields.io/badge/license-AGPL-blue.svg
   :target: https://github.com/searxng/searxng/blob/master/LICENSE

.. |Issues| image:: https://img.shields.io/github/issues/searxng/searxng?color=yellow&label=issues
   :target: https://github.com/searxng/searxng/issues

.. |PR| image:: https://img.shields.io/github/issues-pr-raw/searxng/searxng?color=yellow&label=PR
   :target: https://github.com/searxng/searxng/pulls

.. |commits| image:: https://img.shields.io/github/commit-activity/y/searxng/searxng?color=yellow&label=commits
   :target: https://github.com/searxng/searxng/commits/master

.. |weblate| image:: https://weblate.bubu1.eu/widgets/searxng/-/searxng/svg-badge.svg
   :target: https://weblate.bubu1.eu/projects/searxng/


Contact
=======

Come join us if you have questions or just want to chat about SearXNG.

Matrix
  `#searxng:matrix.org <https://matrix.to/#/#searxng:matrix.org>`_

IRC
  `#searxng on libera.chat <https://web.libera.chat/?channel=#searxng>`_
  which is bridged to Matrix.


Differences to searx
====================

SearXNG is a fork of `searx`_.  Here are some of the changes:

.. _searx: https://github.com/searx/searx


User experience
---------------

- Huge update of the simple theme:

  * usable on desktop, tablet and mobile
  * light and dark versions (you can choose in the preferences)
  * support right-to-left languages
  * `see the screenshots <https://dev.searxng.org/screenshots.html>`_

- the translations are up to date, you can contribute on `Weblate`_
- the preferences page has been updated:

  * you can see which engines are reliable or not
  * engines are grouped inside each tab
  * each engine has a description

- thanks to the anonymous metrics, it is easier to report a bug of an engine and
  thus engines get fixed more quickly

  - if you don't want any metrics to be recorded, you can `disable them on the server
    <https://docs.searxng.org/admin/engines/settings.html#general>`_

- administrator can `block and/or replace the URLs in the search results
  <https://github.com/searxng/searxng/blob/5c1c0817c3996c5670a545d05831d234d21e6217/searx/settings.yml#L191-L199>`_


Setup
-----

- you don't need `Morty`_ to proxy the images even on a public instance
- you don't need `Filtron`_ to block bots, we implemented the builtin `limiter`_
- you get a well maintained `Docker image`_, now also built for ARM64 and ARM/v7 architectures
- alternatively we have up to date installation scripts

.. _Docker image: https://github.com/searxng/searxng-docker


Contributing is easier
----------------------

- readable debug log
- contributions to the themes are made easier, check out our `Development
  Quickstart`_ guide
- a lot of code cleanup and bug fixes
- the dependencies are up to date

.. _Morty: https://github.com/asciimoo/morty
.. _Filtron: https://github.com/searxng/filtron
.. _limiter: https://docs.searxng.org/src/searx.plugins.limiter.html
.. _Weblate: https://weblate.bubu1.eu/projects/searxng/searxng/
.. _Development Quickstart: https://docs.searxng.org/dev/quickstart.html


Translations
============

We need translators, suggestions are welcome at
https://weblate.bubu1.eu/projects/searxng/searxng/

.. figure:: https://weblate.bubu1.eu/widgets/searxng/-/multi-auto.svg
   :target: https://weblate.bubu1.eu/projects/searxng/


Make a donation
===============

You can support the SearXNG project by clicking on the donation page:
https://docs.searxng.org/donate.html
