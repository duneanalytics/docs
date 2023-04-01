[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/alter-view.md)

# ALTER VIEW

## Synopsis

The `ALTER VIEW` command allows for the modification of an existing view in the app. The command can be used to rename a view or change the owner of a view.

``` text
ALTER VIEW name RENAME TO new_name
ALTER VIEW name SET AUTHORIZATION ( user | USER user | ROLE role )
```

## Description

The `ALTER VIEW` command is used to change the definition of an existing view. This command can be used to rename a view or change the owner of a view. Renaming a view is useful when the name of the view no longer accurately reflects the data it contains. Changing the owner of a view is useful when a user or role needs to take ownership of a view.

## Examples

### Renaming a view

To rename a view, use the `RENAME TO` clause followed by the new name of the view. For example, to rename the `people` view to `users`, use the following command:

```
ALTER VIEW people RENAME TO users
```

### Changing the owner of a view

To change the owner of a view, use the `SET AUTHORIZATION` clause followed by the name of the user or role that will become the new owner. For example, to change the owner of the `people` view to user `alice`, use the following command:

```
ALTER VIEW people SET AUTHORIZATION alice
```

## See also

`create-view`{.interpreted-text role="doc"}

This section of the app technical guide covers the `ALTER VIEW` command, which is used to modify an existing view in the app. The guide provides a synopsis of the command, including the syntax and available options. The description explains the purpose of the command and how it can be used to rename a view or change the owner of a view. The examples demonstrate how to use the command to rename a view or change the owner of a view. Finally, the guide provides a reference to the `create-view` command for further information. This guide is located in the `app` folder of the `dune docs` project.
## Questions: 
 1. What is the purpose of this app and how does it relate to blockchain technology?
    - This app technical guide is related to SQL database management and does not have a direct connection to blockchain technology.
2. Can this app be used to manage data stored on a blockchain?
    - It is unclear from this app technical guide whether it can be used to manage data stored on a blockchain or if it is only applicable to traditional SQL databases.
3. Are there any security features built into this app to protect against unauthorized access or tampering of data?
    - The app technical guide does not provide information on any security features or measures implemented in the app.