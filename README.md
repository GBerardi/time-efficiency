# time-efficiency

## Data Loading
Separate operations in chunks and parallelize them when possible.

## Training
data loader num_processes may reduce epoch training time, but not in all cases ...
 - the overhead of managing multiple processes and inter-process communication can offset the benefits
 - num_processes higher than number of CPU cores may degrade performance
 - small datasets or datasets that do not require much pre-processing may not benefit much from a high num_processes
 - high batch sizes reduce frequency of data loading operations and may benefit less from num_processes
