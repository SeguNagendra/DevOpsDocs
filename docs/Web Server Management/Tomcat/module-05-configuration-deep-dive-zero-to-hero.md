---
sidebar_position: 5
title: Configuration Deep Dive
---

# Configuration Deep Dive

In previous modules, you installed Tomcat and deployed applications.

Now we go deeper.

In this module, you will clearly understand:

-   server.xml (heart of Tomcat)
-   Connector configuration
-   Thread settings (maxThreads, acceptCount, maxConnections)
-   context.xml
-   web.xml
-   JNDI basics
-   SSL configuration (basic understanding)
-   GZIP compression
-   Production-safe configuration practices

This module is very important for DevOps engineers.

------------------------------------------------------------------------

# 1. Understanding server.xml

Location:

    conf/server.xml

This is the main configuration file of Tomcat.

It controls:

-   Ports
-   Connectors
-   Thread pool settings
-   Engine
-   Host configuration

If Tomcat is not accessible or misbehaving, server.xml is the first
place to check.

------------------------------------------------------------------------

# 2. Connector Configuration (Very Important)

Inside server.xml, you will see something like:

Connector port="8080"
           protocol="org.apache.coyote.http11.Http11NioProtocol"
           connectionTimeout="20000"
           maxThreads="200"
           redirectPort="8443"

Let's understand each important parameter.

port → Port number where Tomcat listens (default 8080)

protocol → Defines I/O model (NIO recommended)

connectionTimeout → Time (milliseconds) to wait before closing idle
connection

redirectPort → Used when HTTPS is enabled

------------------------------------------------------------------------

# 3. Thread-Related Parameters

maxThreads → Maximum worker threads to process requests

If maxThreads is too low: Requests queue up → slow response

If too high: High memory usage

acceptCount → Number of requests that can wait in queue when all threads
are busy

If queue is full: New requests get rejected

maxConnections → Maximum simultaneous connections allowed

DevOps Tip: Never blindly increase values. Understand server CPU and
memory capacity.

------------------------------------------------------------------------

# 4. Engine, Host, and Context

Inside server.xml:

Engine → Represents processing engine

Host → Virtual host (like domain)

Context → Individual web application

Example:

Host name="localhost" appBase="webapps"

This means applications are loaded from webapps directory.

------------------------------------------------------------------------

# 5. context.xml

Location:

    conf/context.xml

Used for:

-   Defining resources
-   Database connection pooling
-   Application-level settings

Example (JNDI resource):

Resource name="jdbc/MyDB"
          auth="Container"
          type="javax.sql.DataSource"
          maxTotal="100"
          maxIdle="30"
          username="dbuser"
          password="dbpassword"
          driverClassName="com.mysql.cj.jdbc.Driver"
          url="jdbc:mysql://localhost:3306/mydb"

This allows application to connect to database via JNDI.

------------------------------------------------------------------------

# 6. web.xml

Location:

    conf/web.xml

This is global deployment descriptor.

Defines:

-   Default servlet behavior
-   Session timeout
-   MIME mappings
-   Welcome files

Example:

<session-config>
<session-timeout> 30 </session-timeout>
</session-config>

This means session expires after 30 minutes.

------------------------------------------------------------------------

# 7. Enabling HTTPS (Basic Concept)

To enable HTTPS:

Step 1: Create Keystore

    keytool -genkeypair -alias tomcat -keyalg RSA -keystore keystore.jks

Step 2: Modify server.xml

Connector port="8443"
           protocol="org.apache.coyote.http11.Http11NioProtocol"
           SSLEnabled="true"
           keystoreFile="conf/keystore.jks"
           keystorePass="password"
           scheme="https"
           secure="true"

Restart Tomcat.

Now access:

    https://server:8443

In production, usually SSL is handled at Load Balancer.

------------------------------------------------------------------------

# 8. Enabling GZIP Compression

Compression reduces response size.

Add inside Connector:

compression="on" compressionMinSize="1024"
compressibleMimeType="text/html,text/xml,text/plain,text/css,application/json"

This improves performance by reducing bandwidth usage.

------------------------------------------------------------------------

# 9. Production-Safe Configuration Practices

✔ Disable autoDeploy in production\
✔ Do not expose Tomcat directly to internet\
✔ Remove default apps (docs, examples)\
✔ Secure Manager application\
✔ Use proper memory settings\
✔ Monitor thread usage\
✔ Enable access logs

------------------------------------------------------------------------

# 10. Debugging Configuration Issues

If port not accessible: Check Connector port

If app slow: Check maxThreads

If DB connection fails: Check JNDI config

If HTTPS not working: Check keystore path and password

Always restart Tomcat after configuration changes.

------------------------------------------------------------------------

# Summary

After this module, you should:

✔ Understand server.xml structure\
✔ Configure connectors confidently\
✔ Tune thread parameters\
✔ Understand context.xml and web.xml\
✔ Enable HTTPS (basic level)\
✔ Enable compression\
✔ Follow production-safe practices

Next: Logging & Troubleshooting (Zero → Hero).
