Accessing an SSL database from a Java app running in Cloud Foundry
==================================================================

Recently I had a customer with the need to deploy a Tomcat app that used a
MongoDB database in Bluemix. Seems like pretty straightforward, but it isn’t.

The MongoDB offering in Bluemix is called [Compose for
MongoDB](https://console.ng.bluemix.net/docs/services/ComposeForMongoDB/index.html).
Compose is a company IBM acquired a couple of years ago which does
Database-as-a-Service. Through Compose you can get several different databases
in Bluemix, such as MongoDB, PostgreSQL and Redis.

In the cloud world, all serious offerings use SSL for connectivity. Of course,
they are exposing endpoints to the world, it better be SSL. And that’s what
Compose for MongoDB does. So far so good.

In Cloud Foundry, cloud applications leverage the platform ability to bind to
services. When you bind a service to an app in Cloud Foundry, the app has access
to the credentials of the service and there is no need to hard code or use
properties files to connect to backend services, such as a database. The
developers do not need to know the credentials for the database they will be
using, the values are populated in deploy time. This allows for less dependency
on the environment the application will run. So when you bind a Compose for
MongoDB service to an app in Bluemix, the app has access to the username,
password, URL, and the `ca_certificate_base64` property which contains the
certificate it will need to establish a secure connection to the database. That
all looks great, doesn’t it?

Then there’s the catch. Java likes its credentials on a truststore, which is a
file. The certificates need to be loaded in this truststore file and the JVM
needs to know where it is and have access to. But you don’t have access to the
file system in Cloud Foundry. It’s the beauty of the PaaS paradigm. All you care
about are your code and data. The rest is supplied by the cloud provider. In
order to maintain independency of environments you can’t rely on a file system.
Therefore, today, there is no way a Java runtime can read that
`ca_certificate_base64` environment variable, convert it to a certificate and
load it to the truststore. The binding of the service in this case is useless.

In order to achieve this we’ll have to throw the cloud-native approach out the
window and manually create a truststore, put it in the Java project and build a
WAR file that is (unfortunately) specific for that deployment. I’ve posted my
code on [GitHub](https://github.com/macribas/EmployeeDirectory) with some high
level instructions. Feel free to reach out if you need help. I didn’t write the
original app, which is in this [awesome site](https://avaldes.com/) by Amaury
Valdes. I just refactored it to make it run on Cloud Foundry.

DISCLAIMER: By no means this is good example of cloud-native code, it just has
the bare minimum refactoring to make it run on Bluemix.
