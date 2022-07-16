--- 
sidebar_position: 3
title: Permissions
---

## Roles
Roles define the role of `Admin`, `Agents`, and `Users`. Custom roles can also be created if required.

## Permissions
### Tickets
| Perm | Description |
| --- | --- |
| Create | Allow the creation of Tickets |
| View | Allow the viewing of Tickets in which the account has team/group access |
| Update | Allow updating of Tickets in which the account has team/group access  |
| Delete | Allow deleting of Tickets in which the account has team/group access  | 
| --- | --- |
| Print | Allow the printing of tickets. |
| Notes | Allow the creation/viewing of ticket `notes` |
| Manage Public Tickets | Allow the account to access tickets that were submitted without a registered account |
| Can View All Tickets in Assigned Groups | Allow the account to see all tickets in their group. If disabled the account will only see tickets submitted by them.

### Comments
| Perm | Description |
| --- | --- |
| Create | Allow commenting on tickets |
| View | Allow the viewing of comments |
| Update | Allow editing of comments. **Note: [Role Hierarchy](#hierarchy) applies**  |
| Delete | Allow deleting of comments. **Note: [Role Hierarchy](#hierarchy) applies**  | 

### Accounts
| Perm | Description |
| --- | --- |
| Create | Allow the creation of Tickets |
| View | Allow the viewing of Tickets in which the account has team/group access |
| Update | Allow updating of Tickets in which the account has team/group access  |
| Delete | Allow deleting of Tickets in which the account has team/group access  | 
| --- | --- |
| Import | **Requires `Create`** Allows importing of accounts from `JSON`, `CSV`, & `LDAP` |

### Groups
| Perm | Description |
| --- | --- |
| Create | Allow creating of customer groups |
| View | Allow viewing of customer groups |
| Update | Allow editing of customer groups  |
| Delete | Allow the deletion of customer groups  | 

### Teams
| Perm | Description |   
| --- | --- |
| Create | Allow creating of agent teams |
| View | Allow viewing of agent teams |
| Update | Allow editing of agent teams  |
| Delete | Allow the deletion of agent teams  | 

### Departments
| Perm | Description |
| --- | --- |
| Create | Allow creating of agent departments |
| View | Allow viewing of agent departments |
| Update | Allow editing of agent departments  |
| Delete | Allow the deletion of agent departments  | 

### Reports
| Perm | Description | 
| --- | --- |
| Create | Allow creating of reports |
| View | Allow viewing of reports |
| Update | Allow editing of reports  |
| Delete | Allow the deletion of reports  | 

### Notices
| Perm | Description |
| --- | --- |
| Create | Allow creating of notices |
| View | Allow viewing of notices |
| Update | Allow editing of notices  |
| Delete | Allow the deletion of notices  | 
| --- | --- |
| Activate | Allow activation of notices/announcements |
| Deactivate | Allow notices/announcements to be deactivated |

## Hierarchy
Permission Hierarchy is designed to allow any role which falls below the given role to have permissions over that role resources. 
:::note Default Behavior
By default, this allows the `Admin` role to edit/update tickets submitted by the `Agent` or `User` role and the `Agent` role to edit/update tickets submitted by the `User` role.
:::

:::info Note
This only applies if the role has the apporiate permissions enabled.
:::
