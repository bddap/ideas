A neural network architecture that dynamically chooses its own shape at inference time.

# Dynamic Tangle

- Submodule (generic): A connectable unit, a node within a tangle. Dynamic tangles are generic over submodule type. Submodule could be a vanilla rectangular feed forward network, or even another tangle.
- Dynamic Tangle: A collection of submodules with paths between defined at inference time by a tangle controller. The tangle is by necessity a directed acyclic graph.
- Tangle Controller (generic): Outputs at inference time, the set of active paths between submodules.

## Example

Let each `Sn` be a submodule

```
Controller
S1, S2, S3
```

The controller has one scalar "enable" output for submodule ancestor pair. During inference, each "enable" output is treated as a weight connecting the two submodules.

```
Controller outputs: [S1->S2, S1->S3, S2->S3]
```

## Recurrent Mode

When the tangle controller can connect submodules to non-ancestors, allowing loops.

```
Controller: [S1->S1, S1->S2, S1->S3, S2->S1, S2->S2, S3->S3, S3->S1, S3->S2, S3->S3]
S1, S2, S3
```

## Output

The output of one or multiple submodules in the tangle may be passed to as output from the tangle.
In recurrent mode, edges may be reassigned by feeding output[s] to the controller.

## Fickle Mode

In fickle mode, the controller receives outputs from all submodules. Each submodule is invoked, the controller observes all outputs and assigns topology for the next iteration.

Fickle mode is parallelizable because messages aren't passed between multiple nodes during a single iteration. For example, assume these connections `S1->S2, S2->S3`. In fickle mode, information will not pass from `S1` to `S3` in a single iteration.

(In fickle mode should the controller even exist? maybe it should output the same shape as its inputs and be fed directly back into the submodules.)

## Partial Fickle Mode

Controller need not be invoked every iteration. Partial fickle Mode re-assigns topology every `n` loops instead of every loop, where `n` is an integer larger than one.
