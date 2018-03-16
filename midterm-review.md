#### 1. Give an example of demand for computation speed
NOAA’s Weather and Climate Operational Supercomputer System need computation speed to analyze tons of data to support atmospheric and   water prediction sciences and services.

#### 2. In a  sentence, define speedup
- Parallel Speedup: How much faster the program becomes once some computing resources are added
- Parallel Efficiency: Ratio of performance improvement per individual unit of computing resource
- Given $p$ processors, speedup, $S(p)$ is calculated as the ratio of the time it takes to run the program using a single processor over the time it takes to run the program using p processor.

#### 3. In a sentence, define efficiency
The efficiency $E$ is then defined as the ratior of speedup over the number of processors, $p$.

#### 4. Describe two limiting factors in achieving maximum parallelism
- Non-parallelizable code
- Communication overhead

#### 5. Describe linear speedup?  What types of applications will exhibit linear speedup?

#### 6. What is superlinear speedup?  What can cause superlinear speedup?
- Sometimes a speedup of more than A when using A processors is observed in parallel computing, which is called super-linear speedup.
- With the larger accumulated cache size, more or even all of the working set can fit into caches and the memory access time reduces dramatically, which causes the extra speedup in addition to that from the actual computation.
- performing backtracking in parallel
- parallel implementations of branch-and-bound for optimization:[7] the processing of one node by one processor may affect the work other processors need to do for the other nodes.

#### 7. In a sentence, define Amdahl’s Law.  Give the equation for Amdahl’s Law.
- Amdahl's law is a formula which gives the theoretical speedup in latency of the execution of a task at fixed workload that can be expected of a system whose resources are improved.
- S = P/( (P-1)F+1 )

 #Suppose that 4% of my application is serial.  
 #What is my predicted speedup according to Amdahl’s Law on 5 processors?
- f = 0.04
- E = 1/((5 - 1)*f + 1)
- print (E)
- print (E * 5)

## 8. Suppose that I get a speedup of 8 when I run my application on 10 processors.  According to Amdahl's Law, what portion is serial?  What is the speedup on 20 processors?  What is the efficiency?  What is the best speedup that I could hope for?

- 8 = 10 / [(10 - 1)*F + 1]  ==> 9F = 0.25
- S= 20 / [(20-1)*F +1 ]   ==> S= 20/(19*0.25/9+1) = 13.09
- E = 13.09 / 20 = 65.45%
- BEST SPEEDUP = 36

#### 9. Suppose that 4% of my application is serial.  What is my predicted speedup according to Amdahl’s Law on 5 processors?
 #Suppose that 4% of my application is serial.  
 #What is my predicted speedup according to Amdahl’s Law on 5 processors?
  f = 0.04
  E = 1/((5 - 1)*f + 1)
  print (E)
  print (E * 5)
  0.8620689655172414
  4.310344827586207
  
#### 10. For each of the following type of parallel computers, briefly describe its architecture, provide its schematic, and name a programming model
- SIMD
- Shared memory
- Distributed memory – message passing
- Distributed shared memory

#### 11. Briefly describe the three benchmarking procedures: LINPACK, HPCC, SHOC
  LINPACK makes use of the BLAS (Basic Linear Algebra Subprograms) libraries for performing basic vector and matrix operations.
  HPCC: HPC Challenge is a benchmark suite that measures a range memory access patterns. 
  - HPL (LINPACK to solve linear system of equation) 
  - DGEMM (Double Precision General Matric Multiply)
  - STREAM (Memory bandwidth)
  - PTRANS (Parallel Matrix Transpose to measure processors communication)
  - RandomAccess (Random memory updates)
  - FFT (double precision complex discrete fourier transform)
  - Communication bandwidth and latency
  SHOC: The Scalable Heterogeneous Computing Benchmark Suite (SHOC) is a collection of benchmark programs testing the performance and stability of systems using computing devices with non-traditional architectures for general purpose computing, and the software used to program them. Its initial focus is on systems containing Graphics Processing Units (GPUs) and multi-core processors, and on the OpenCL programming standard. It can be used on clusters as well as individual hosts.
  - Non-traditional systems (GPU)
  
#### 12. Briefly describe the three supercomputing rankings: TOP500, GREEN500, GRAPH500
- TOP500: Rank the supercomputers based on their LINPACK score
- GREEN500: Rank the supercomputers with emphasis on energy usage (LINPACK / power consumption)
- GRAPH500: Rank systems based on benchmarks degisned for data-intensive computing

#### 13. Give the command to load the gcc compiler version 5.3.0 and the openmpi library version 10.3.1 into your environment
module load gcc/5.3.0 openmpi/1.10.3

#### 14. What is a message tag?
*tag* is an integer identify the message. MPI_Recv will only place data in the buffer if the tag from MPI_Send matches. The constant MPI_ANY_TAG may be used when the source tag is unknown or not important. "

#### 15. What is an MPI communicator?  What is the purpose of the communicator?
A communicator is an object describing a group of processes. In many applications all processes work together closely coupled, and the only communicator you need is MPI_COMM_WORLD , the group describing all processes that your job starts with.

An important reason for using communicators is the development of software libraries. If the routines in a library use their own communicator (even if it is a duplicate of the outside communicator), there will never be a confusion between message tags inside and outside the library.

#### 16. In MPI, what is a process rank? What routine do you use to determine a process rank?
Unique IDs (rank) are defined for individual processes within a communicator group
Ranks are used to enforce execution/exclusion of code segments within the original source code
Ranks can be used as mean to calculate and distributed workload (data) among the processes

#### 17. True or false:  In MPI you set the number of processes when you write the source code.
False, you assign the number of process when you run the script.

#### 18. Explain the basic functionality of the collective calls Bcast, Scatter, Gather, Barrier, Reduce, and how they are the same or different from each other.
- bcast : data = comm.bcast(data, root=0)  --> broadcast data to all other nodes.
- scatter: partial_data = comm.scatter(data, root=0) 
  Data are divided according to rank;
- gather: Data arrive and are sorted at root according to rank
  all_data = comm.gather(data, root=0)
- reduce: <final result at sending process> = comm.reduce(<data to be reduced>, op=MPI.<operation>, root=<root process>
  sum = comm.reduce(rank, op=MPI.SUM, root=0)
  if rank == 0:
    print ("The reduction is %s" % (sum))
  #run on 5 nodes, the output is " the reduction is 10 "
- Barrier:?
  comm.barrier()
  Synchronization operation
  Every process in communicator group must execute before any can leave
  Try to avoid this if possible


#### 19. With a short sentence, describe the role of MPI.COMM_WORLD
   a handle to a group of process. MPI_COMM_WORLD: - Contains all of the processes.

#### 20. What is “Pleasantly Parallel?” List two characteristics of pleasantly parallel
   pleasantly parallel
“A computation that can obviously be divided into a number of completely different parts, each of which can be executed by a separate process.”

#### 21. Describe three workload assignment approaches for pleasantly parallel using a few sentences for each approach
Start with small number of processes
Calculation workload assignment manually for each count of processes
Generalize assignment for process i based on sample calculations

#### 22. How do the worker processes know when to terminate in the dynamic workload assignment model?
?
#### 23. With a short sentence each, describe the two basic partitioning approaches in parallel programming.
?

#### 24. A scientist wants to calculate the sum of 8,192 integers. The scientist has a 16-cores CPU that takes 0.1ns to transfer one integer from one core to another. Construct a tree that describes the divide-and-conquer process to calculate the sum. Calculate the communication time the “divide” period and the communication time for the “conquer” period.
?

#### 25. Given 8 processes ranked 0 through 7, sort the following array of integers in ascending order using the odd-even transposition sorting process. You should clearly indicate which integers belong to which process at every single stage of the sorting process. [13, 7, 14, 11, 10, 4, 15, 12, 3, 6, 16, 1, 2, 8, 9, 5]

#### 26. Be prepared to answer programming questions of the following type:      

- Using only MPI_Send and MPI_Recv, implement MPI_Reduce.
- Using only MPI_Send and MPI_Recv, implement MPI_Scatter.
- Using only MPI_Send and MPI_Recv, implement MPI_Gather.
- Using only MPI_Send and MPI_Recv, implement MPI_Alltoall.

#### 31. Give an example of a master/slave computation using MPI-like pseudocode.
Master/Slave Architecture:
- Master: NameNode
- Workers: Data Node    
NameNode:
- manages the file system namespace
- regulates access to files by clients
- executes file system namespace operations
- determines the mapping of blocks to DataNodes
DataNode:
- one per node in the cluster
- manages storage attached to the node
- serves read and write requests clients
   
#### 32. Understand and be able to read/trace through all codes discussed in class lectures.
#### 33. Understand the principles of the communication tree among the processes in divide-and-conquer problems.
#### 34. What are the four main characteristics of Parallel File Systems?
Single namespace, including files and directories hierarchy
Actual data are distributed over storage servers
--Only large files are split up into contiguous data regions
Metadata regarding namespace and data distribution are stored:
--Dedicated metadata servers (PVFS)
--Distributed across storage servers (CephFS)
#### 35. What are the two main differences between block-based and object-based parallel file systems?
BLOCK-BASED-Objects are created as fixed-width blocks
- File growth requires more blocks
- Blocks distributed over storage nodes
- Suffer from block allocation issues, lock managers
- Example: GPFS

OBJECT-BASED-Objects are created as variable-length regions of the file
- A file has a constant number of objjects
- File growth increases the size of the object(s)
- Space allocation is managed locally on a per-object basis
- Potential issue with workload imbalance
- Example: Lustre, PVFS
