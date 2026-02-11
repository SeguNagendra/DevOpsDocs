---
sidebar_position: 8
title: Security Hardening
---

# Security Hardening

Security is not optional in production.

If Tomcat is not secured properly:

-   Attackers may access manager console
-   Sensitive data may leak
-   Server version may be exposed
-   Default apps may be exploited
-   SSL misconfiguration may expose traffic

As a DevOps engineer, your responsibility is to make Tomcat
production-safe.

In this module, you will clearly understand:

-   Removing default applications
-   Securing Tomcat Manager
-   Disabling unnecessary HTTP methods
-   Hiding server information
-   File permission best practices
-   SSL certificate handling basics
-   Security headers basics
-   Basic vulnerability awareness
-   Production hardening checklist

------------------------------------------------------------------------

# 1. Remove Default Applications

After fresh installation, Tomcat includes:

-   docs
-   examples
-   manager
-   host-manager

Location:

    webapps/

In production, remove unnecessary applications:

    rm -rf webapps/docs
    rm -rf webapps/examples

Why?

Default apps may expose information or become attack surface.

Production servers should run only required applications.

------------------------------------------------------------------------

# 2. Secure Tomcat Manager Application

Tomcat Manager allows:

-   Deploy/undeploy apps
-   Restart applications
-   View sessions

Never expose it publicly.

To configure access:

Edit:

    conf/tomcat-users.xml

Add:
```
role rolename="manager-gui"
user username="admin" password="StrongPassword123" roles="manager-gui"
```
Best Practices:

-   Use strong passwords
-   Restrict access by IP (using firewall or reverse proxy)
-   Avoid exposing port 8080 to internet

------------------------------------------------------------------------

# 3. Disable TRACE Method

TRACE can expose request headers.

Disable in web.xml:
```
Add inside `<web-app>`{=html}:
`<security-constraint>`{=html} `<web-resource-collection>`{=html}
`<web-resource-name>`{=html}Disable TRACE`</web-resource-name>`{=html}
`<url-pattern>`{=html}/\*`</url-pattern>`{=html}
`<http-method>`{=html}TRACE`</http-method>`{=html}
`</web-resource-collection>`{=html} `<auth-constraint />`{=html}
`</security-constraint>`{=html}
```
Restart Tomcat after change.

------------------------------------------------------------------------

# 4. Hide Server Version Information

By default, response headers may show:

Server: Apache-Coyote/1.1

This reveals version information.

To hide server version:

In server.xml Connector, add:

    server=""

Example:

\<Connector port="8080" server="" ... /\>

This prevents version exposure.

------------------------------------------------------------------------

# 5. File Permission Best Practices

Tomcat should not run as root.

Create dedicated user:

    useradd -r tomcat

Change ownership:

    chown -R tomcat:tomcat /opt/tomcat

Set proper permissions:

    chmod -R 750 /opt/tomcat



Why?

If Tomcat compromised while running as root, entire system is at risk.

------------------------------------------------------------------------

# 6. SSL Certificate Management (Basic Level)

If HTTPS configured directly in Tomcat:

-   Store keystore securely
-   Use strong password
-   Restrict file access

Check certificate expiry regularly.

If certificate expires: Browser shows security warning.

In production, SSL is often terminated at Load Balancer.

------------------------------------------------------------------------

# 7. Security Headers Basics

Security headers protect against common attacks.

Example headers:

X-Frame-Options X-Content-Type-Options Content-Security-Policy
Strict-Transport-Security

These can be configured in:

-   Application level
-   Reverse proxy (Nginx/Apache)

Better practice: Configure at reverse proxy layer.

------------------------------------------------------------------------

# 8. Firewall & Network-Level Security

Never expose Tomcat port directly to internet.

Best architecture:

Internet → Load Balancer → Reverse Proxy → Tomcat (private network)

Allow only required ports:

80 / 443 (public) 8080 (internal only)

Use security groups / firewall rules properly.

------------------------------------------------------------------------

# 9. Basic Vulnerability Awareness

Security risks may arise from:

-   Outdated Tomcat version
-   Weak passwords
-   Exposed management endpoints
-   Default configurations

Always:

-   Keep Tomcat updated
-   Monitor CVE announcements
-   Patch regularly

Security is ongoing process, not one-time setup.

------------------------------------------------------------------------

# 10. Production Hardening Checklist

Before moving to production, verify:

✔ Default apps removed\
✔ Manager secured\
✔ Strong passwords used\
✔ Tomcat not running as root\
✔ Proper file permissions\
✔ SSL configured correctly\
✔ Server version hidden\
✔ TRACE disabled\
✔ Firewall rules validated\
✔ Logs monitored

Security should be reviewed periodically.

------------------------------------------------------------------------

# Summary

After completing this module, you should:

✔ Secure Tomcat installation properly\
✔ Remove unnecessary applications\
✔ Protect management interfaces\
✔ Understand basic SSL handling\
✔ Apply safe file permissions\
✔ Hide server details\
✔ Follow structured hardening checklist

Next: High Availability & Scaling
