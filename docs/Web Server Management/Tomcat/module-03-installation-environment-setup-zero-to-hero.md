---
sidebar_position: 3
title: Installation & Environment Setup
---

# Installation & Environment Setup

In this module, you will learn how to properly install Apache Tomcat and
understand every step clearly.

We will cover:

-   Why Java is required
-   Installing Java
-   Installing Tomcat
-   Understanding Tomcat directory structure
-   Environment variables (JAVA_HOME, CATALINA_HOME, CATALINA_BASE)
-   Starting and stopping Tomcat
-   Running Tomcat as a system service
-   Managing multiple environments (Dev / QA / Prod)
-   Changing ports
-   Common startup failures and fixes

This module builds real operational confidence.

------------------------------------------------------------------------

# 1. Why Java is Required

Apache Tomcat is written in Java.

That means: - It runs inside JVM (Java Virtual Machine) - JVM executes
Tomcat's code - Without Java, Tomcat cannot start

First check if Java is installed:

    java -version

If Java is not installed:

For RHEL / CentOS: sudo yum install java-17-openjdk

For Ubuntu: sudo apt install openjdk-17-jdk

After installation:

    which java
    readlink -f $(which java)

This helps you find the actual Java installation directory.

------------------------------------------------------------------------

# 2. Understanding JAVA_HOME

JAVA_HOME tells Tomcat where Java is installed.

Example:

    export JAVA_HOME=/usr/lib/jvm/java-17-openjdk

Why this is important:

When Tomcat starts, it checks JAVA_HOME. If not set correctly, Tomcat
fails with error like:

"JAVA_HOME is not defined correctly"

Best practice: Add JAVA_HOME to \~/.bashrc or /etc/profile for
persistence.

------------------------------------------------------------------------

# 3. Downloading and Installing Tomcat

Step 1: Download Tomcat from official website.

Example:

    wget https://downloads.apache.org/tomcat/tomcat-9/...

Step 2: Extract it:

    tar -xvzf apache-tomcat-9.x.x.tar.gz

Step 3: Move to standard location:

    sudo mv apache-tomcat-9.x.x /opt/tomcat

Now your Tomcat directory is:

    /opt/tomcat

------------------------------------------------------------------------

# 4. Understanding Tomcat Directory Structure

Inside Tomcat directory:

bin/\
→ Startup and shutdown scripts

conf/\
→ Configuration files (server.xml, web.xml)

lib/\
→ Shared libraries

logs/\
→ Log files

webapps/\
→ Deployed applications (WAR files)

temp/\
→ Temporary files

work/\
→ Compiled JSP files

Understanding these directories is critical for debugging.

------------------------------------------------------------------------

# 5. CATALINA_HOME vs CATALINA_BASE

CATALINA_HOME: → Main Tomcat installation directory

CATALINA_BASE: → Instance-specific configuration

Why this matters:

If running multiple Tomcat instances on same server, you should separate
CATALINA_BASE for each environment.

Example:

/opt/tomcat (CATALINA_HOME) /opt/tomcat-dev (CATALINA_BASE)
/opt/tomcat-qa /opt/tomcat-prod

This allows multiple instances without conflict.

------------------------------------------------------------------------

# 6. Starting and Stopping Tomcat

Go to bin directory:

    cd /opt/tomcat/bin

Start:

    ./startup.sh

Stop:

    ./shutdown.sh

After starting, verify:

    netstat -tulnp | grep 8080
    or
    ss -lntp | grep 8080

Open in browser:

    http://server-ip:8080

If page loads, Tomcat is running.

------------------------------------------------------------------------

# 7. Running Tomcat as a Systemd Service

In production, we should not start Tomcat manually.

Create file:

    /etc/systemd/system/tomcat.service

Basic structure:

\[Unit\] Description=Apache Tomcat After=network.target

\[Service\] Type=forking User=tomcat Group=tomcat
Environment=JAVA_HOME=/usr/lib/jvm/java-17-openjdk
Environment=CATALINA_HOME=/opt/tomcat
ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

\[Install\] WantedBy=multi-user.target

Reload systemd:

    systemctl daemon-reload
    systemctl start tomcat
    systemctl enable tomcat

Now Tomcat starts automatically on boot.

------------------------------------------------------------------------

# 8. Changing Default Port (8080)

Default HTTP port is 8080.

To change:

Edit:

    conf/server.xml

Find Connector:

    Connector port="8080" ... 

Change to:

    Connector port="9090" ... 

Restart Tomcat.

Always ensure firewall allows new port.

------------------------------------------------------------------------

# 9. Managing Multiple Environments (Dev / QA / Prod)

Never use same configuration everywhere.

Best practice:

-   Separate config files
-   Separate ports
-   Separate logs
-   Separate JVM memory settings

Example:

Dev: - Lower memory - Debug logs enabled

Prod: - Optimized memory - INFO log level - SSL enabled

------------------------------------------------------------------------

# 10. Common Startup Failures & Fixes

Problem 1: Port already in use Solution: netstat -tulnp \| grep 8080

Kill conflicting process.

Problem 2: JAVA_HOME not set Solution: export JAVA_HOME properly

Problem 3: Permission denied Solution: chown -R tomcat:tomcat
/opt/tomcat

Problem 4: OutOfMemoryError Solution: Increase JVM memory in setenv.sh:

    export CATALINA_OPTS="-Xms512m -Xmx1024m"

------------------------------------------------------------------------

# Summary

After completing this module, you should:

✔ Install Java confidently\
✔ Install Tomcat properly\
✔ Understand directory structure\
✔ Set environment variables correctly\
✔ Start/Stop Tomcat\
✔ Run as system service\
✔ Manage multiple environments\
✔ Fix common startup problems

Next: Deployment & Release Engineering (Zero → Hero).
