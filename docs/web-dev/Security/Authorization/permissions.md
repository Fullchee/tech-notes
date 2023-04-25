# [Permissions](https://fullchee-reminders.netlify.app/link/1119)

https://auth0.com/blog/permissions-privileges-and-scopes/

## Access Control

> selective restriction of access to a resource

![user-app-resource-relationship.png](user-app-resource-relationship.png)

User wants to access a resource

-   example: access your Google Calendar

App mediates access to that resource

## Permission

-   an action that can be executed on a resource
-   on the resource
    -   without Google Calendar, can't have a permission to access Google Calendar

## Privilege

![privileges-permissions-user.png](privileges-permissions-user.png)

-   privileges given to a user/app
    -   privileges have permissions (which are on the resource)

## Scopes

What an app can do on behalf of the user

-   example: read/write

### Scopes vs Privileges

Scopes: NOT just privileges for apps

-   scopes are always on behalf of a user
    -   privileges must be checked when scopes are used
    -   if the user loses the privileges, the scope should reflect that

There are scopes that aren't in the resource permissions or the user privileges

examples

-   OpenID scope
-   return an ID token as the result of the user auth
-   profile, email, address, phone

### Scopes vs Permissions

-   some permissions can't be delegated
-   can't be added to a scope
    -   example: never allow an app to delete a calendar event

![permissions-privileges-scopes](permissions-privileges-scopes.jpeg)

## Forma permissions

Permissions ↔ Roles ↔ Group ↔ User

all many to many relationships

Group and User are Django built-ins

Roles are kinda like privileges

We don't have the notion of scopes

### Why Groups weren't enough

Permissions on individual resources

dashboard_etl_manager.branch_view-sync

Role examples

-   Dashboard Admin
-   Approvals Admin
