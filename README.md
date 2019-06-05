**Work in progress**

# Minimal reactive library in C

## Planned features

> The `rc_` prefix stands for React C

### Call function(s) when a variable's values has changed

```c
uint32_t id = rc_var_create(RC_VAR_TYPE_INT + 32);

int32_t x = 4;
rc_var_set(id, &x);
rc_var_set_int(id, x);

int32_t * xp = rc_var_get(id);
```

Types:
- `RC_VAR_TYPE_POINTER`
- `RC_VAR_TYPE_INT[8/16/32]`
- `RC_VAR_TYPE_UINT[8/16/32]` 
- `RC_VAR_TYPE_BUF[X]`

```c
typedef enum
{
  RC_VAR_TYPE_POINTER = 0x10
  RC_VAR_TYPE_BOOL =    0x11
  RC_VAR_TYPE_CHAR =    0x12
  RC_VAR_TYPE_INT =     0x200,
  RC_VAR_TYPE_UINT =    0x300,
  RC_VAR_TYPE_BUF =     0x1000,
}rc_var_type_t
```

E.g. `RC_VAR_TYPE_INT + 32` will be stored as `0x100 + 32 = 0x120`. The base and the size can be masked out.


The basic value set function is:
```c
rc_var_set(id, &x);
```

But there are some helpers
```c
rc_var_set_int(id, -13);
rc_var_set_uint(id, 39);
rc_var_set_bool(id, true);
rc_var_set_char(id, 'a');
rc_var_set_str(id, "some text");
rc_var_set_buf(id, buf);
```

It also can work:
```c
my_stuct_t * s = rc_var_get(id);
s.num = 3;
rc_var_refr(id);
```

### Work with or without dynamic memory allocation

TODO

### Function(s) can subscribe to listen a variable change

TODO

### Simple integration

Only a `rc_handler()` needs to be called periodically in an:
- task
- main `while(1)`
- a Timer intrrupt (on embedded systems)
