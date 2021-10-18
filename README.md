# Helm chart for ProxySQL

This helm chart creates a ProxySQL Cluster in Kubernetes. This is useful if you have applications running in Kubernetes that rely on external MySQL server(s). Once installed, you can manage ProxySQL like you would any other ProxySQL installation.

# Usage

This chart is not yet available for adding to helm. To use this chart, you must clone this repository to your system. Once cloned, I recommend grabbing the default values used during installation:

`helm show values proxysql-kubernetes > proxysql.yaml`

You can then edit the values file to suit your environment. You may find the defaults are perfectly fine for testing.

For production use you will want to change the default passwords. Unless you configure your cluster otherwise, ProxySQL will be available to anyone looking around A strong password on the admin user is a must.

To install ProxySQL into your cluster, the command might look like this:

`helm install proxysql -f proxysql.yaml proxysql-kubernetes`

This will install ProxySQL Cluster into Kubernetes. By default, you will get three instances distributed as evenly as possible within your cluster if you have more than one worker.

# Accessing the administrative interface

You can access the administrative interface, and configure ProxySQL using one of two methods. You can simply shell into a running copy of ProxySQL and connect to 127.0.0.1 using the mysql client OR create a utility pod with MySQL client tools installed. If you choose to use a utility pod you will connect to the service "proxysql-headless" (or, if you used a different name during installation check your services listing for the headless service pointed to "controller") using the cluster admin user information located in the values.yaml file.

# Accessing ProxySQL

ProxySQL will be exposed as a service in your cluster. If, at install, you name your installation "proxysql" the service will be named proxysql. It will be on port 6033. Connect to this service like you would any other MySQL server.

# How to configure ProxySQL

For information on how to configure and use ProxySQL, visit their offical documentation at https://proxysql.com/documentation/.
