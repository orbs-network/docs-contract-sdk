# Data types \(Exported Functions\)

Data types refer to arguments in **public** functions and their return values. All non exported functions can use any Go type \(notice that only white-listed package will compile\). There are currently 16 types that are supported: 8 basic types \(called here 'scalar'\) and their 8 slice versions. Please note: alias or named types of these should not be used.

You may use any arithmetic, calculation, operand or function that is allowed or exists in Go. 

## The 'Scalar' types:

1\) `uint32` - a 32 bit unsigned integer

2\) `uint64` - a 64 bit unsigned integer.

3\) `string` - a string .

4\) `[]byte` - a blob of data in slice of bytes. Can represent address and hashes too.

5\) `bool` - a bit of data.

6\) `*big.Int` - Go type that is used for very large integers up to 256 bit \(referred sometimes as uint256\)

7\) `[20]byte` - a fixed size array of 20 bytes. This is very useful to represent addresses in  cryptography.

8\) `[32]byte` - a fixed size array of 32 bytes. This is very useful for signatures and hashes in cryptography.

It is possible to run any arithmetic operation which exists in Go.

## The 'Slice' types:

1\) `[]uint32` - a slice of 32 bit unsigned integers

2\) `[]uint64` - a slice of 64 bit unsigned integers

3\) `[]string` - a slice of strings 

4\) `[][]byte` - a slice of blobs of data.

5\) `[]bool` - a slice of bits of data.

6\) `[]*big.Int` - a slice of very large integers. 

7\) `[][20]byte` - a slice of arrays of 20 bytes.

8\) `[][32]byte` - a slice of arrays of 32 bytes.



