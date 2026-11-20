# LDAP Authentication plug-in

This is a simple LDAP authentication plug-in for Mirth Connect. It can be used
to allow users to login using an LDAP service for authentication and authorization.

You can also fall-back to using the local Mirth user-database if you'd like if
no acceptable user can be located in the LDAP service.

## Configuration

Configuration is done using a simple Java properties file, `ldap.properties`,
which you place on your server alongside your `mirth.properties` file (the
engine's `conf/` directory). A sample file is included in this directory, and it
contains comments describing each configuration setting. The plug-in logs the
file it loaded at start-up; changes take effect when the engine restarts.

If `ldap.url` or `ldap.group-filter` is missing, LDAP is skipped and everyone
signs in with their local engine password, so a missing or broken file can't
lock out the local administrator. The start-up log says so. Users listed in
`ldap.non-ldap-usernames` always use their local password.

Users who sign in with LDAP get an engine user created for them the first time
(unless `ldap.auto-create-users=false`), without the Administrator's first-login
dialog. A failed sign-in shows the same message whatever the reason (wrong
password, not in the required group, no engine user); the reason is in the
engine's log.

## Installation

Simply upload the ZIP file containing the plug-in via the Mirth Connect
administrator, or unzip the ZIP file into the `extensions/` directory on
your Mirth server.

## Building

The LDAP authenticator can be built with Apache Maven, but it will require that
you obtain a few libraries manually, since Mirth Connect does not public Maven
artifacts. You will need to place these files into the `libs/` directory:

    mirth-server.jar

You can find these libraries in Mirth Connect's server download.
