# Docker compose packet

# Create and run all services except monitored machines

This docker-composed project created for microservice architecture (hereinafter in text as `application`).

Main application task is remote controlling of Windows machines via PowerShell by SSH. Event logs for every PC processed via WinLogBeat and Logstash.
Project includes:
- 5 python services
- Web server
- Logstash instance
- PostgreSQL instance
- RabbitMQ instanse as broker for services

Names of files and services was changed and some unrelated data such pipelines and configs were removed.

### Preparing to run:

1. Copy services codes to according directories `/services/code/<service_name>/`

2. Fill configs for services `/services/conf/`

3. Fill pipline config for Logstash `/logstash/pipeline/logstash.conf`

4. `.env` config file 
    - USERNAME - username that will be used for connect by ssh  
    - PIP_PROXY - proxy for pip if needed
    - POSTGRES_USER - db user will be used for connection
    - POSTGRES_PASSWORD - db password will be used for connection
    - POSTGRES_DB - db name will be used for connection
    - RABBITMQ_DEFAULT_USER - broker user will be used for connection
    - RABBITMQ_DEFAULT_PASS - broker password will be used for connection

5. `/ubuntu/passwd` file
    - it is needed for correct work services using ubuntu image
    - fill it with correct username (`env:USERNAME`)

6. `/ubuntu/.ssh/`
    - place here ssh-related files
    - all linked files are needed (for example: it was tested with no 
   known_hosts file - does not work properly)
    - this files related to user `env:USERNAME`

7. Dockerfiles for services that use ubuntu images have `env:http_proxy`

8. Change permissions for whole packet directory

### Run:

`sudo docker-compose up --build`

