Connect to repo API
==============================================

What is the cloud repo API?
------------------------------

The repo API stores details about pipes needed to pull/push data. There are alternatives to the cloud API, covered in advanced sections, but the cloud repo API is the best way to get started.

Register user and login
------------------------------

To use the cloud repo API, you need to register which you can do from inside python. See :doc:`registration <../quickstart>`

Now that you are registered you can :doc:`pull files <../pull>`.

Setting Proxy
------------------------------

If you are behind a proxy, you may have to set your proxy to connect to the repo API.

.. code-block:: python

    import os
    cfg_proxy = "http://yourip:port"
    os.environ["http_proxy"] = cfg_proxy; os.environ["HTTP_PROXY"] = cfg_proxy;
    os.environ["https_proxy"] = cfg_proxy; os.environ["HTTPS_PROXY"] = cfg_proxy;


Advanced Topics
---------------------------------------------

Managing your cloud API token
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Run the below if you forgot your token or need to reset. 

.. code-block:: python

    # retrieve token
    api.forgotToken('your-username','password')

    # reset token
    api = d6tpipe.api.APIClient(token=None)
    api.register('your-username','your@email.com','password')


Local Mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The best way to get started is to use the cloud API. As an alternative to the cloud API, you can use d6tpipe in local mode which stores all details locally. That is fast and secure, but limits functionality.  

.. code-block:: python

    import d6tpipe
    api = d6tpipe.api.APILocal() # local mode

Local mode requires you to manage more settings on your own (see below). Particularly you need to manage protocols and remote directories on your own. Additionally, there is no pipe setting inheritance.

.. code-block:: python

    # s3
    settings['protocol']='s3'
    settings['options']={'remotepath': 's3://bucketname/foldername'}
    d6tpipe.upsert_pipe(api, settings)
    settings['parent']='pipe-parent' # won't do anything


Local vs Server Mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The local mode stores everything locally so nothing ends up in the cloud. While that is fast and secure, it limits functionality. Only the server can:  

* automatically manage remote paths
* provide pipe inheritance
* manage permissions
* share data across teams and organizations
* remotely scan for file changes and centrally cache results
* regularly check for file changes on a schedule
* remotely mirror datasets, eg from ftp to S3

Overall the way you interface with d6tpipe very similar between the two modes so you can easily switch between them. So you can start in local mode and then switch to server mode to take advantage of advanced features.

Onprem repo API
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can deploy an onprem repo API to take advance of server functionality without using the cloud server, contact <support@databolt.tech> for details.
