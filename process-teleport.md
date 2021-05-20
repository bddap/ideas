# Summary

Using wasm as an example. Expose a function, `teleport()`, to a wasm module. When the module calls `teleport()`, the host enviroment halts local execution of the module. It then serializes the wasm module along with its entire state. The serialized wasm module is sent to a remote host. The remote host begins interpreting the wasm module where the previous host left off.

From the perspective of the wasm module, it called `teleport()` and it was instantly running on a different host.

# Uses?

Perhaps one host has fast low-latency access to hardware that another host does not. The average distance from earth to Mars is 751 light seconds.

Extreme multithreading.
