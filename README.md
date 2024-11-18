# time-efficiency

## Data Loading
Separate operations in chunks and parallelize them when possible.

Multi process parallelism (copy of the memory for every process):
```
given a function, an iterable of func input and a chunksize that splits the input data
in chunks for each process
    with mp.Pool(num_processes) as p:
        results = p.starmap(function, 
                            iterable,
                            chunksize)
```

## Loops and repeated calls
- Reduce the operations inside a loop or a function that is called many times to the only needed ones.
Everything that can be done in a different part of the code should be moved away.
- Avoid array operations inside loops as they are normally very costly (array creation, append, ...)

## Training
Data loader num_workers may reduce epoch training time, but not in all cases ...
 - the overhead of managing multiple processes and inter-process communication can offset the benefits
 - num_workers higher than number of CPU cores may degrade performance
 - small datasets or datasets that do not require much pre-processing may not benefit much from a high num_workers
 - high batch sizes reduce frequency of data loading operations and may benefit less from num_workers

## Code complexity
Minimize innested loops (reducing O(n^2) to O(n) for example)
  - Is it possible to move an inner loop outside the outer loop (running it a single time instead of repeating the loop at every iteration of the outer loop) ?
  - Does a function call in a loop hide a loop ? Is it possible to substitute the function call ?


## Multi processing
Ones a loop is reduced to his minimum (low complexity and only the needed operations) you can:
- log the time required
- if the time is high you can consider to parallelize it (in python multiprocessing or multithreading)
