# mysql

Contains a configuration to spin up a MySQL instance inside a kubernetes cluster.

## Prerequisites

* kind
* kubectl
* MySQL client

Note: Depending on the OS, it may be necessary to prefix all commands with `sudo`.

## Configuration

1.  Create the `kind` cluster:
    ```shell
    kind create cluster --name=mysql --config=kind/config.yaml
    ```
    
2.  Set the cluster config:
    ```shell
    kubectl cluster-info --context kind-mysql
    ```

3.  Deploy the MySQL instance:
    ```shell
    kubectl apply -k k8s/local/
    ```

## Usage

### Access from localhost

To access the MySQL cluster from your machine port-forwarding can be used.

1.  Start port-forwarding:
    ```shell
    kubectl port-forward service/mysql-service 30306:3306 
    ```
    
2.  Open a separate terminal and use the MySQL client to connect:
    ```shell
    mysql -u root -p -h localhost --protocol=tcp --port=30306
    ```
    Enter `admin` as the password when prompted.
