 .. Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

 ..   http://www.apache.org/licenses/LICENSE-2.0

 .. Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.



Google Cloud Storage Operators
==============================

Cloud Storage allows world-wide storage and retrieval of any amount of data at any time.
You can use Cloud Storage for a range of scenarios including serving website content,
storing data for archival and disaster recovery, or distributing large data objects to users via direct download.

See :doc:`/operators/transfer/index` for a list of specialized transfer operators to and from Google Cloud Storage.

Prerequisite Tasks
^^^^^^^^^^^^^^^^^^

.. include:: /operators/_partials/prerequisite_tasks.rst

Operators
^^^^^^^^^

.. _howto/operator:GCSTimeSpanFileTransformOperator:

GCSTimeSpanFileTransformOperator
--------------------------------

Use the
:class:`~airflow.providers.google.cloud.operators.gcs.GCSTimeSpanFileTransformOperator`
to transform files that were modified in a specific time span (the data interval).
The time span is defined by the time span's start and end timestamps. If a DAG
does not have a *next* DAG instance scheduled, the time span end infinite, meaning the operator
processes all files older than ``data_interval_start``.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_transform_timespan.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_gcs_timespan_file_transform_operator_Task]
    :end-before: [END howto_operator_gcs_timespan_file_transform_operator_Task]


.. _howto/operator:GCSBucketCreateAclEntryOperator:

GCSBucketCreateAclEntryOperator
-------------------------------

Creates a new ACL entry on the specified bucket.

For parameter definition, take a look at
:class:`~airflow.providers.google.cloud.operators.gcs.GCSBucketCreateAclEntryOperator`

Using the operator
""""""""""""""""""

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_acl.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_gcs_bucket_create_acl_entry_task]
    :end-before: [END howto_operator_gcs_bucket_create_acl_entry_task]

Templating
""""""""""

.. literalinclude:: /../../google/src/airflow/providers/google/cloud/operators/gcs.py
    :language: python
    :dedent: 4
    :start-after: [START gcs_bucket_create_acl_template_fields]
    :end-before: [END gcs_bucket_create_acl_template_fields]

More information
""""""""""""""""

See Google Cloud Storage Documentation to `create a new ACL entry for a bucket
<https://cloud.google.com/storage/docs/json_api/v1/bucketAccessControls/insert>`_.

.. _howto/operator:GCSObjectCreateAclEntryOperator:

GCSObjectCreateAclEntryOperator
-------------------------------

Creates a new ACL entry on the specified object.

For parameter definition, take a look at
:class:`~airflow.providers.google.cloud.operators.gcs.GCSObjectCreateAclEntryOperator`

Using the operator
""""""""""""""""""

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_acl.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_gcs_object_create_acl_entry_task]
    :end-before: [END howto_operator_gcs_object_create_acl_entry_task]

Templating
""""""""""

.. literalinclude:: /../../google/src/airflow/providers/google/cloud/operators/gcs.py
    :language: python
    :dedent: 4
    :start-after: [START gcs_object_create_acl_template_fields]
    :end-before: [END gcs_object_create_acl_template_fields]

More information
""""""""""""""""

See Google Cloud Storage insert documentation to `create a ACL entry for ObjectAccess
<https://cloud.google.com/storage/docs/json_api/v1/objectAccessControls/insert>`_.


.. _howto/operator:GCSListObjectsOperator:

GCSListObjectsOperator
----------------------

Use the
:class:`~airflow.providers.google.cloud.operators.gcs.GCSListObjectsOperator`
to list objects in a Google Cloud Storage bucket. Optionally specify a prefix to list only objects whose
names begin with that prefix, and a delimiter to emulate directory-like organization.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_copy_delete.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_gcs_list_bucket]
    :end-before: [END howto_operator_gcs_list_bucket]

.. _howto/operator:GCSDeleteObjectsOperator:

GCSDeleteObjectsOperator
------------------------

Use the
:class:`~airflow.providers.google.cloud.operators.gcs.GCSDeleteObjectsOperator`
to delete one or more objects from a Google Cloud Storage bucket.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_copy_delete.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_gcs_delete_object]
    :end-before: [END howto_operator_gcs_delete_object]

.. _howto/operator:GCSDeleteBucketOperator:

Deleting Bucket
^^^^^^^^^^^^^^^

Deleting Bucket allows you to remove bucket object from the Google Cloud Storage.
It is performed through the
:class:`~airflow.providers.google.cloud.operators.gcs.GCSDeleteBucketOperator` operator.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_upload_download.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_gcs_delete_bucket]
    :end-before: [END howto_operator_gcs_delete_bucket]


You can use :ref:`Jinja templating <concepts:jinja-templating>` with
:template-fields:`airflow.providers.google.cloud.operators.gcs.GCSDeleteBucketOperator`
parameters which allows you to dynamically determine values.

Reference
---------

For further information, look at:

* `Client Library Documentation <https://googleapis.dev/python/storage/latest/buckets.html>`__
* `Product Documentation <https://cloud.google.com/storage/docs/json_api/v1/buckets>`__

Sensors
^^^^^^^

.. _howto/sensor:GCSObjectExistenceSensor:

GCSObjectExistenceSensor
------------------------

Use the :class:`~airflow.providers.google.cloud.sensors.gcs.GCSObjectExistenceSensor` to wait (poll) for the existence of a file in Google Cloud Storage.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_sensor.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_object_exists_task]
    :end-before: [END howto_sensor_object_exists_task]

Also you can use deferrable mode in this operator if you would like to free up the worker slots while the sensor is running.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_sensor.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_object_exists_task_defered]
    :end-before: [END howto_sensor_object_exists_task_defered]

.. _howto/sensor:GCSObjectsWithPrefixExistenceSensor:

GCSObjectsWithPrefixExistenceSensor
-----------------------------------

Use the :class:`~airflow.providers.google.cloud.sensors.gcs.GCSObjectsWithPrefixExistenceSensor` to wait (poll) for the existence of a file with a specified prefix in Google Cloud Storage.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_sensor.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_object_with_prefix_exists_task]
    :end-before: [END howto_sensor_object_with_prefix_exists_task]

You can set the ``deferrable`` param to True if you want this sensor to run asynchronously, leading to more
efficient utilization of resources in your Airflow deployment. However the triggerer component needs to be enabled
for this functionality to work.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_sensor.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_object_with_prefix_exists_task_async]
    :end-before: [END howto_sensor_object_with_prefix_exists_task_async]


.. _howto/sensor:GCSUploadSessionCompleteSensor:


GCSUploadSessionCompleteSensor
------------------------------

Use the :class:`~airflow.providers.google.cloud.sensors.gcs.GCSUploadSessionCompleteSensor` to check for a change in the number of files with a specified prefix in Google Cloud Storage.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_sensor.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_gcs_upload_session_complete_task]
    :end-before: [END howto_sensor_gcs_upload_session_complete_task]

You can set the parameter ``deferrable`` to True if you want the worker slots to be freed up while sensor is running.


.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_sensor.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_gcs_upload_session_async_task]
    :end-before: [END howto_sensor_gcs_upload_session_async_task]

.. _howto/sensor:GCSObjectUpdateSensor:

GCSObjectUpdateSensor
---------------------

Use the :class:`~airflow.providers.google.cloud.sensors.gcs.GCSObjectUpdateSensor` to check if an object is updated in Google Cloud Storage.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_sensor.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_object_update_exists_task]
    :end-before: [END howto_sensor_object_update_exists_task]

You can set the ``deferrable`` param to True if you want this sensor to run asynchronously, leading to efficient
utilization of resources in your Airflow deployment. However the triggerer component needs to be enabled
for this functionality to work.

.. exampleinclude:: /../../google/tests/system/google/cloud/gcs/example_gcs_sensor.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_object_update_exists_task_async]
    :end-before: [END howto_sensor_object_update_exists_task_async]

More information
""""""""""""""""

Sensors have different modes that determine the behaviour of resources while the task is executing.
See `Airflow sensors documentation
<https://airflow.apache.org/docs/apache-airflow/stable/concepts.html#sensors>`_ for best practices when using sensors.


Reference
^^^^^^^^^

For further information, look at:

* `Client Library Documentation <https://googleapis.github.io/google-cloud-python/latest/storage/index.html>`__
* `Product Documentation <https://cloud.google.com/storage/docs/>`__
