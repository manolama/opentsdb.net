/api/config
===========

This endpoint returns information about the running configuration of the TSD. It is read only and cannot be used to set configuration options.

Verbs
-----

* GET
* POST

Requests
--------

This endpoint does not require any parameters via query string or body.

Example Request
^^^^^^^^^^^^^^^

**Query String**
::
  http://localhost:4242/api/config
   
Response
--------
   
The response is a hash map of configuration properties and values.

.. NOTE:: When a configuration setting with the string "pass" is found, the value for that property will be replaced with "\*\*\*\*\*\*\*\*". This is a trivial means of obfuscating passwords.

Example Response
^^^^^^^^^^^^^^^^
.. code-block :: javascript 

  {
      "tsd.core.auto_create_metrics": "true",
      "tsd.core.meta.enable_realtime_ts": "false",
      "tsd.core.meta.enable_realtime_uid": "false",
      "tsd.core.meta.enable_tsuid_incrementing": "false",
      "tsd.core.meta.enable_tsuid_tracking": "true",
      "tsd.core.plugin_path": "/usr/local/opentsdb/plugins",
      "tsd.core.tree.enable_processing": "true",
      "tsd.http.cachedir": "/tmp/opentsdb",
      "tsd.http.request.cors_domains": "",
      "tsd.http.request.enable_chunked": "true",
      "tsd.http.request.max_chunk": "16384",
      "tsd.http.show_stack_trace": "true",
      "tsd.http.staticroot": "/usr/local/opentsdb/staticroot/",
      "tsd.mq.enable": "true",
      "tsd.network.async_io": "true",
      "tsd.network.bind": "0.0.0.0",
      "tsd.network.keep_alive": "true",
      "tsd.network.port": "4242",
      "tsd.network.reuse_address": "true",
      "tsd.network.tcp_no_delay": "true",
      "tsd.network.worker_threads": "",
      "tsd.rpc.plugins": "net.opentsdb.tsd.DummyRpcPlugin",
      "tsd.rpcplugin.DummyRPCPlugin.hosts": "localhost",
      "tsd.rpcplugin.DummyRPCPlugin.port": "42",
      "tsd.rtpublisher.enable": "true",
      "tsd.rtpublisher.plugin": "net.opentsdb.tsd.RabbitMQPublisher",
      "tsd.rtpublisher.rabbitmq.hosts": "127.0.0.1",
      "tsd.rtpublisher.rabbitmq.pass": "********",
      "tsd.rtpublisher.rabbitmq.user": "guest",
      "tsd.rtpublisher.rabbitmq.vhost": "/",
      "tsd.search.elasticsearch.hosts": "127.0.0.1",
      "tsd.search.elasticsearch.tsmeta_type": "tsmetadata",
      "tsd.search.enable": "false",
      "tsd.search.enableindexer": "false",
      "tsd.search.plugin": "net.opentsdb.search.ElasticSearch",
      "tsd.search.tree.indexer.enable": "true",
      "tsd.stats.canonical": "true",
      "tsd.storage.enable_compaction": "false",
      "tsd.storage.flush_interval": "1000",
      "tsd.storage.hbase.data_table": "tsdb",
      "tsd.storage.hbase.meta_table": "tsdb-meta",
      "tsd.storage.hbase.tree_table": "tsdb-tree",
      "tsd.storage.hbase.uid_table": "tsdb-uid",
      "tsd.storage.hbase.zk_basedir": "/hbase",
      "tsd.storage.hbase.zk_quorum": "127.0.0.1"

  }
