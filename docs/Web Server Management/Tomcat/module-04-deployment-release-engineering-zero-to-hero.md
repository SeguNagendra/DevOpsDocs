---
sidebar_position: 4
title: Deployment & Release Engineering
---

# Deployment & Release Engineering

In this module, you will learn how applications are deployed into
Tomcat.

We will clearly understand:

-   What is a WAR file
-   Internal structure of a WAR
-   Different deployment methods
-   Context paths
-   Auto deployment
-   Tomcat Manager deployment
-   Basic zero-downtime idea
-   Common deployment failures and fixes

This module connects development output (WAR file) to production server.

------------------------------------------------------------------------

# 1. What is a WAR File?

WAR = Web Application Archive

It is a compressed package (like ZIP) that contains:

-   Java classes
-   JSP files
-   HTML/CSS/JS
-   Libraries (JAR files)
-   Configuration files

Developers build WAR file using tools like Maven or Gradle.

As DevOps, you deploy this WAR into Tomcat.

------------------------------------------------------------------------

# 2. Internal Structure of WAR

If you extract a WAR file:

    jar -xvf app.war

You will see:

/META-INF /WEB-INF index.jsp other static files

Important folders:

WEB-INF/ → Contains classes and libraries

WEB-INF/classes/ → Compiled Java classes

WEB-INF/lib/ → JAR dependencies

Important: Files inside WEB-INF cannot be accessed directly via browser.

------------------------------------------------------------------------

# 3. Manual Deployment (Simplest Method)

Step 1: Copy WAR into webapps folder:

    cp app.war /opt/tomcat/webapps/

Step 2: Tomcat automatically extracts WAR.

After extraction:

/webapps/app/

Access application:

    http://server:8080/app

This is called context path.

------------------------------------------------------------------------

# 4. Context Path Explained

If WAR name is:

    myapp.war

Context path becomes:

    http://server:8080/myapp

If you want root application:

Rename WAR to:

    ROOT.war

Then access:

    http://server:8080/

Understanding context path avoids 404 confusion.

------------------------------------------------------------------------

# 5. Auto Deployment

Tomcat monitors webapps directory.

If you:

-   Add WAR → It deploys
-   Replace WAR → It redeploys
-   Delete WAR → It undeploys

Auto deployment is convenient for Dev/QA.

In production: Often disabled for better control.

Configured in server.xml:

autoDeploy="true" deployOnStartup="true"

------------------------------------------------------------------------

# 6. Tomcat Manager Deployment

Tomcat provides Manager application.

Access:

    http://server:8080/manager/html

You can:

-   Deploy WAR via browser
-   Undeploy application
-   Reload application

To enable Manager access:

Edit conf/tomcat-users.xml

Add:

`role rolename="manager-gui"
`user username="admin" password="strongpassword" roles="manager-gui"

Restart Tomcat.

Security Tip: Never expose manager directly to internet.

------------------------------------------------------------------------

# 7. Redeployment & Downtime

When WAR is replaced:

-   Old application stops
-   New version starts

During this time: Users may face short downtime.

This is acceptable in Dev. In production, we use better strategy.

------------------------------------------------------------------------

# 8. Basic Zero-Downtime Idea (Beginner Level)

Instead of one Tomcat:

Use two Tomcat instances behind Load Balancer.

Flow:

Instance A → Active\
Instance B → Deploy new version

Switch traffic to B. Then update A.

This is basic Blue-Green approach.

Prevents full downtime.

------------------------------------------------------------------------

# 9. Common Deployment Failures

Problem 1: 404 Not Found Cause: Wrong context path.

Problem 2: 500 Internal Server Error Cause: Application error or missing
dependency.

Check logs:

    tail -f logs/catalina.out

Problem 3: ClassNotFoundException Cause: Missing JAR in WEB-INF/lib

Problem 4: Port conflict Cause: Another service using 8080

------------------------------------------------------------------------

# 10. Deployment Debug Checklist

If app not accessible:

1.  Check WAR present in webapps
2.  Check extraction happened
3.  Check logs for errors
4.  Check port open
5.  Check firewall
6.  Check context path
7.  Check DB connectivity

Always debug layer by layer.

------------------------------------------------------------------------

# Summary

After this module, you should confidently:

✔ Understand WAR file structure\
✔ Deploy application manually\
✔ Use Tomcat Manager\
✔ Understand context paths\
✔ Understand auto deployment\
✔ Know beginner zero-downtime concept\
✔ Debug deployment failures

Next: Configuration Deep Dive (server.xml, context.xml, web.xml).
