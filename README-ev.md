## Cloud Controller

* cloud_controller.yml

        app_uris:
          # Allow applications to register URIs that are outside your domain.
          allow_external: true
          reserved_list: [www, test, dash, register, foo, bar, everglade, feedhenry]
          reserved_length: 3
    
        uaa:
          enabled: true
          url: http://uaa.<domain>

## DEA

* dea.yml

        # Secure environment for running applications in a multi tenant setup.
        secure: true
        
        runtimes:
          - ruby18
          - ruby19
          - ruby193
          - node
          - node06
          - node08


## Runtimes

* runtimes.yml - only ruby & node runtimes

## Stager

* stager.yml

        secure: true

Need to ensure vcap-stager-users are created.

    cd vcap/stager/
    sudo bundle install
    cd bin
    sudo ./create_secure_users.rb
    cat /etc/passwd

Verify users in passwd file e.g.

    vcap-stager-user-1:x:23001:120::/nonexistent:/bin/false
    vcap-stager-user-2:x:23002:120::/nonexistent:/bin/false
    vcap-stager-user-3:x:23003:120::/nonexistent:/bin/false
    vcap-stager-user-4:x:23004:120::/nonexistent:/bin/false
    vcap-stager-user-5:x:23005:120::/nonexistent:/bin/false
    vcap-stager-user-6:x:23006:120::/nonexistent:/bin/false

## UAA

* uaa.yml

        uaa:
          uris:
            - uaa.<domain>
            - login.<domain>

## Components

* router
* stager
* cloud_controller
* health_manager
* dea
* uaa
* redis_node
* mysql_node
* redis_gateway
* mysql_gateway

## Stuff that should be changed

        vcap@ip-10-32-40-210:~/cloudfoundry/.deployments/devbox/config$ grep -r "change" .
        ./redis_gateway.yml:token: changeredistoken
        ./postgresql_backup.yml:  pass: changeme
        ./mysql_gateway.yml:token: changemysqltoken
        ./filesystem_gateway.yml:token: changefilesystemtoken
        ./postgresql_node.yml:  pass: changeme
        ./rabbitmq_gateway.yml:token: changerabbitmqtoken
        ./vblob_gateway.yml:token: changevblobtoken
        ./health_manager.yml:    password: changeme
        ./uaa.yml:    password: changeme
        ./mongodb_gateway.yml:token: changemongodbtoken
        ./cloud_controller.yml:    password: changeme
        ./cloud_controller.yml:    token: changemysqltoken
        ./cloud_controller.yml:    token: changeredistoken
        ./cloud_controller.yml:    token: changemongodbtoken
        ./cloud_controller.yml:    token: changerabbitmqtoken
        ./cloud_controller.yml:    token: changepostgresqltoken
        ./cloud_controller.yml:    token: changevblobtoken
        ./cloud_controller.yml:    token: changefilesystemtoken
        ./cloud_controller.yml:  token: ["changebrokertoken"]
        ./postgresql_gateway.yml:token: changepostgresqltoken
