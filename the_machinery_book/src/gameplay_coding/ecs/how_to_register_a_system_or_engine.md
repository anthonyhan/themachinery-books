# Registering a System or an Engine

To register Systems/Engines, you need to provide a register function to the `tm_entity_register_engines_simulation_i` interface. This function has the signature:

```c
{{$include {TM_BOOK_CODE_SNIPPETS}/gameplay_code/ecs_system_engine.c:14}}
```

For more information check the `tm_entity_register_engines_simulation_i` .

Whenever the Machinery creates an Entity Context, it calls this function and registers all your Systems / Engines to this context.

> The Entity context is the world in which all your entities exist.

For Engines, you pass an instance of the `tm_entity_system_i` to the register function.

```c
// example:
{{$include {TM_BOOK_CODE_SNIPPETS}/gameplay_code/ecs_system_engine.c:14:32}}
```



For Systems, you pass an instance of the `tm_engine_i` to the register function.

```c
{{$include {TM_BOOK_CODE_SNIPPETS}/gameplay_code/ecs_system_engine.c:39:49}}
```

In the above example the scheduler will schedule this system after the `maze_generation_system` system! Since we did not provide any further information in `.writes` or in `.components` the scheduler has no other information to work with. In this case it is best to not write anything!

*Example load function:*


```c
TM_DLL_EXPORT void tm_load_plugin(struct tm_api_registry_api *reg, bool load)
{
    // other code ...
{{$include {TM_BOOK_CODE_SNIPPETS}/gameplay_code/ecs_system_engine.c:55}}
}
```



## Register your system or engine to the Editor

You can use the `tm_entity_register_engines_simulation_i` to register your engine or system to an entity context that runs only in the Editor. This might be good for components that shall only be used in the Editor.

The function signature is the same as the for the other interface!



### Register systems & engines outside of the load function

You also can register your System/Engine outside of the load function wherever you have access to the correct Entity Context.



