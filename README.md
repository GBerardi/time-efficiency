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


## Training
data loader num_workers may reduce epoch training time, but not in all cases ...
 - the overhead of managing multiple processes and inter-process communication can offset the benefits
 - num_workers higher than number of CPU cores may degrade performance
 - small datasets or datasets that do not require much pre-processing may not benefit much from a high num_workers
 - high batch sizes reduce frequency of data loading operations and may benefit less from num_workers
