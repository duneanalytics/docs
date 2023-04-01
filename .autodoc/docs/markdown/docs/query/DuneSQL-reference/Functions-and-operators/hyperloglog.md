[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/hyperloglog.md)

# HyperLogLog Functions

This technical guide is focused on the `app` folder of the Dune Docs project and covers the implementation of the `approx_distinct` function using the HyperLogLog data structure in Trino. The guide provides an overview of the data structures, serialization, and functions used in the implementation.

## Data Structures

Trino implements HyperLogLog data sketches as a set of 32-bit buckets that store a maximum hash. These sketches can be stored sparsely or densely. The HyperLogLog data structure starts as the sparse representation, switching to dense when it is more efficient. The P4HyperLogLog structure is initialized densely and remains dense for its lifetime.

## Serialization

Data sketches can be serialized to and deserialized from `varbinary`. This allows them to be stored for later use. Combined with the ability to merge multiple sketches, this allows one to calculate `approx_distinct` of the elements of a partition of a query, then for the entirety of a query with very little cost.

## Functions

The guide provides an overview of the following functions:

### approx_set()

**``approx_set(x)``** → HyperLogLog

Returns the `HyperLogLog` sketch of the input data set of `x`. This data sketch underlies `approx_distinct` and can be stored and used later by calling `cardinality()`.

### cardinality()

**``cardinality(hll)``** → bigint

This function performs `approx_distinct` on the data summarized by the `hll` HyperLogLog data sketch.

### empty_hll()

**``empty_hll()``** → HyperLogLog

Returns an empty `HyperLogLog`.

### merge()

**``merge(hyperloglog)``** → HyperLogLog

Returns the `HyperLogLog` of the aggregate union of the individual `hll` HyperLogLog structures.

The guide also provides an example of how to use these functions to calculate weekly or monthly unique users by combining daily unique users using `approx_set()` and `merge()`. The example also shows how to store the `HyperLogLog` sketch in `varbinary` format and use `cardinality()` to calculate the approximate distinct count. 

Overall, this guide provides a comprehensive overview of the HyperLogLog functions used in Trino and how they can be used to efficiently calculate approximate distinct counts.
## Questions: 
 1. What is the advantage of using HyperLogLog data sketches for approximating distinct values in Trino? 
   
   Answer: A blockchain SQL analyst might want to know the advantage of using HyperLogLog data sketches in Trino for approximating distinct values. The app technical guide explains that HyperLogLog data sketches are implemented as a set of 32-bit buckets that store a maximum hash, and they can be stored sparsely or densely, which makes them more efficient. 

2. How can data sketches be serialized and deserialized in Trino? 

   Answer: A blockchain SQL analyst might want to know how data sketches can be serialized and deserialized in Trino. The app technical guide explains that data sketches can be serialized to and deserialized from `varbinary`, which allows them to be stored for later use. 

3. What are some use cases of `approx_distinct` with `GROUPING SETS` that can be converted to use `HyperLogLog` in Trino? 

   Answer: A blockchain SQL analyst might want to know some use cases of `approx_distinct` with `GROUPING SETS` that can be converted to use `HyperLogLog` in Trino. The app technical guide explains that `approx_distinct` can be used to calculate the `HyperLogLog` for daily unique users, which allows weekly or monthly unique users to be calculated incrementally by combining the dailies.