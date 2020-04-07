# Data Engineering DevTools
This project's main focus is complete automation of Data Engineering (DE) tool Deployment.

Instead of spending frustrating hours on tool installation and configuration, you can clone this repos and run the attached Ansible playbook. 
This repository lets you to be five commands away from writing ELT code with a modern Data Infrastructure tool stack.

This repository leverages Ansible's Declarative Infrastructure as Code (IaC) to install and configure DE tools.

<img src="https://github.com/angelddaz/de-devtools/blob/master/images/20200406screenshot.png" width="70%" height="70%">

### Tool Focus
* Operating System: Ubuntu 18.04 
* Languages
    * Python 3
    * PostgreSQL 10
* Open Source Software
    * Airflow
* Cloud
    * AWS CLI 

All tools are open source or free tiers. Reference: https://free-for.dev/#/
## Future Tools:
* Spark
* [dbt](https://www.getdbt.com/)

### Software Dependencies
```bash
sudo apt-get update && apt-get install -y software-properties-common git
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt-get install -y ansible
```
Ubuntu:18.04 Operating System

### PostgreSQL Database Object Conflicts
Make sure you do not have a local Postgres Database and Roles called `airflow`.

## Download and Installation
Downloading the playbook to install your Data Engineering tools.
```bash
git clone https://github.com/angelddaz/de-devtools ~/de-devtools
ansible-playbook ~/de-devtools/main.yml
```

## Running Installed Tools
### Airflow
1. Build the downloaded and configured puckel docker image
```bash
cd ~/de-devtools/docker-airflow
docker build .
```
2. Run a preconfigured container off of the built image
```bash
# still in ~/de-devtools/docker-airflow
docker-compose -f docker-compose-LocalExecutor.yml up -d
```

#### Airflow notes:
Create and Edit DAGs here:
* `~/de-devtools/airflow_home/dags` 

**(Optional)** Make an alias in your `~/.bashrc` file for easier [CLI](https://airflow.apache.org/docs/stable/cli.html) usage `airflow [subcommand]`: 
* `alias airflow=docker run --rm -it puckel/docker-airflow airflow'
UI here: 
* [localhost:8080](http://localhost:8080/)

## Testing
Building a docker image and running a docker container.
```bash
# Creates image
docker build -t de-devtools .
# run container on image
docker run --rm -it de-devtools /bin/bash
```

Following Ansible Syntax best practices with built in linter
```bash
ansible-lint main.yml
```
