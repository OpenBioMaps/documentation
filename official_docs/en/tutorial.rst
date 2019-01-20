Tutorials
*********

Upload data
===========
`Upload interface usage: Video tutorial (balkanherps example) english <https://youtu.be/qsu-0UeC46g>`_

`Upload interface usage: Video tutorial (Milvus general forms) română <https://www.youtube.com/watch?v=BknizNC8pvc&t=102s>`_

`Upload interface usage: Video tutorial (Milvus atlas form) română <https://www.youtube.com/watch?v=kFnSxYp4zNM&t=33s>`_

`Upload interface usage: Video tutorial (Milvus nocturnal birds form) română <https://www.youtube.com/watch?v=NmuIdfsXYjk>`_

Query Data
==========

Share Data
==========

New project
===========

Database access
===============

Virtual servers
===============

Docker
------

Prepare/Install Docker & Composer

Detailed docker install documents:

  https://docs.docker.com/compose/install/

Steps:

1) sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

2) sudo chmod +x /usr/local/bin/docker-compose

3) docker-compose --version



OBM docker install

1) git clone git@gitlab.com:openbiomaps/docker/obm-composer.git

2) cd obm-composer/

3) docker-compose up -d

  * http://localhost:9880/biomaps/
  * http://localhost:9880/biomaps/projects/sablon/

Management

Update (after small changes in application)

* docker-compose pull 
* docker-compose up -d

Stopping docker

docker-compose down

Drop everything (including data and databases)

docker-compose down -v

Shell access of web app

docker-compose exec app bash

Reading logs

docker-compose logs -f app

Resources
* https://gitlab.com/openbiomaps/web-app
* https://gitlab.com/openbiomaps/docker
* https://hub.docker.com/r/gaspara/obm-web-app

VirtualBox
----------
