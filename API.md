# API examples and usage

## Statements with parameters

To pass parameters to a statement, use `neo4j_map_entry_t` and `neo4j_map`. For example, from `src/bin/authentication.c`:

```C
neo4j_map_entry_t param = neo4j_map_entry("password", neo4j_string(password)); // password is a char*
neo4j_run(connection, "CALL dbms.changePassword({password})", neo4j_map(&param, 1));  // &param is a pointer to an array of entries of size 1
```
