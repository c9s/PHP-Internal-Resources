PHP Extension Code Snippets
===========================

## PHP function

### Basic function skeleton

```c
PHP_FUNCTION(extension_function1)
{

    RETURN_NULL;
}
```

### Function with parameters

```php
<?
function hello( $array, $string, mixed $optional ) {

}
```

```c
PHP_FUNCTION(hello)
{
    zval *routeset;
    char *path;
    int  path_len;
    zval *z_subpats = NULL;	/* Array for subpatterns */

    /* parse parameters */
    if (zend_parse_parameters(ZEND_NUM_ARGS() TSRMLS_CC, "as|z", 
                    &routeset, 
                    &path, &path_len,
                    &z_subpats
                    ) == FAILURE) {
        RETURN_FALSE;
    }

    RETURN_STRING("Hello World", 1);
}
```

## Variable

A variable is a zval, run ALLOC_INIT_ZVAL to alloc and initialize a zval variable.

```c
zval *z_val;
ALLOC_INIT_ZVAL( z_val );
```






### Get request method

    /* get request method */
    char *c_request_method;
    int  c_request_method_len;
    zval **z_server_hash;
    zval **z_request_method;

	if (zend_hash_find(&EG(symbol_table), "_SERVER", sizeof("_SERVER"), (void **) &z_server_hash) == SUCCESS &&
		Z_TYPE_PP(z_server_hash) == IS_ARRAY &&
		zend_hash_find(Z_ARRVAL_PP(z_server_hash), "REQUEST_METHOD", sizeof("REQUEST_METHOD"), (void **) &z_request_method) == SUCCESS
	) {
		c_request_method = Z_STRVAL_PP(z_request_method);
        c_request_method_len = Z_STRLEN_PP(z_request_method);

        // convert to lower case, for comparing string
        php_strtolower(c_request_method ,c_request_method_len);
	}


