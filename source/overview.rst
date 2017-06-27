========
概述
========

项目与版本
=====================

Scrapy可以管理多个项目，每个项目可以有多个上传的版本，但是只有最新版本才能用来启动新的爬虫。

A common (and useful) convention to use for the version name is the revision
number of the version control tool you're using to track your Scrapy project
code. For example: ``r23``. The versions are not compared alphabetically but
using a smarter algorithm (the same `distutils`_ uses) so ``r10`` compares
greater to ``r9``, for example.

Scrapyd是如何工作的
=================

Scrapyd是一个监听对爬虫的请求并对每一个请求启动一个进程的应用程序，这个进程会执行以下命令::

    scrapy crawl myspider

Scrapyd也支持并行运行多个进程, allocating them in a fixed
number of slots given by the :ref:`max_proc` and :ref:`max_proc_per_cpu` options,
starting as many processes as possible to handle the load.

In addition to dispatching and managing processes, Scrapyd provides a
:ref:`JSON web service <api>` to upload new project versions
(as eggs) and schedule spiders. This feature is optional and can be disabled if
you want to implement your own custom Scrapyd. The components are pluggable and
can be changed, if you're familiar with the `Twisted Application Framework`_
which Scrapyd is implemented in.

Starting from 0.11, Scrapyd also provides a minimal :ref:`web interface
<webui>`.

开始使用Scrapyd
================

To start the service, use the ``scrapyd`` command provided in the Scrapy
distribution::

    scrapyd

That should get your Scrapyd started.

调度并运行爬虫
=======================

To schedule a spider run::

    $ curl http://localhost:6800/schedule.json -d project=myproject -d spider=spider2
    {"status": "ok", "jobid": "26d1b1a6d6f111e0be5c001e648c57f8"}

For more resources see: :ref:`api` for more available resources.

.. _webui:

Web接口
=============

Scrapyd comes with a minimal web interface (for monitoring running processes
and accessing logs) which can be accessed at http://localhost:6800/

.. _distutils: http://docs.python.org/library/distutils.html
.. _Twisted Application Framework: http://twistedmatrix.com/documents/current/core/howto/application.html
.. _server command: http://doc.scrapy.org/en/latest/topics/commands.html#server
