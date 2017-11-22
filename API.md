# API examples and usage

## Statements with parameters

To pass parameters to a statement, use `neo4j_map_entry_t` and `neo4j_map`. For example, from `src/bin/authentication.c`:

```C
neo4j_map_entry_t param = neo4j_map_entry("password", neo4j_string(password)); // password is a char*
neo4j_result_stream_t *results = neo4j_run(connection, "CALL dbms.changePassword({password})", neo4j_map(&param, 1));  // &param is a pointer to an array of entries of size 1
```
To create a simple node, you could, for example:

```C
neo4j_map_entry_t nodeId = neo4j_map_entry("nodeId", neo4j_int(1));
neo4j_result_stream_t *results = neo4j_run(connection, "CREATE (n:Node {id:{nodeId}})", neo4j_map(&nodeId, 1));
```

_Remember to `neo4j_close_results` to close the stream._

## Fetching results

```C
neo4j_result_t *result = neo4j_fetch_next(results);
if (result == NULL) {
	neo4j_perror(stderr, errno, "Failed to fetch result");
}

neo4j_value_t value = neo4j_result_field(result, 0);
char buf[128];
printf("%s\n", neo4j_tostring(value, buf, sizeof(buf)));
```
