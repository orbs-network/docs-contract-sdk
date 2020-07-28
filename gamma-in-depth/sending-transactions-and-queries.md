# Sending transactions and queries

## Using Gamma CLI

Transactions are different from read-only queries by the fact they're able to change state. Transactions require consensus by several nodes whereas read-only queries can rely on a single node.

Send transactions to contracts by running `gamma-cli send-tx` and giving a JSON file containing the call arguments.

For example, to send the transaction with arguments in **transfer.json**

```text
gamma-cli send-tx transfer.json -signer user1
```

Perform queries and call read-only contract methods by running `gamma-cli run-query` and giving a similar JSON file.

For example, to make the read call with arguments in **get-balance.json**

```text
gamma-cli run-query get-balance.json -signer user1
```

## Command parameters

```text
gamma-cli send-tx <INPUT_FILE> -arg# [OVERRIDE_ARG_#] -signer [ID_FROM_KEYS_JSON]
```

```text
gamma-cli run-query <INPUT_FILE> -arg# [OVERRIDE_ARG_#] -signer [ID_FROM_KEYS_JSON]
```

* `<INPUT_FILE>` Path of the JSON file containing the call arguments
* `-signer` Account ID of the signer of the call \(from `orbs-test-keys.json`\)
* `-arg#` Override the value of argument number \# from the input call argument JSON

## Call argument JSON

This simple JSON file is used to let Gamma CLI know which contract method should be executed and what arguments should be passed to it.

An example of such a JSON is

```javascript
{
  "ContractName": "CounterExample",
  "MethodName": "add",
  "Arguments": [
    {
      "Type": "uint64",
      "Value": "25"
    }
  ]
}
```

The **ContractName** should be the name chosen during deployment of the contract with `gamma-cli deploy`. The method name should be one of the exported methods found in the contract source code.

The array of arguments should be given according to the declaration of the method in contract source code.

### Supported argument types

* `uint32` - Integer with 32 bit precision. Matches the `uint32` type in Go contracts. Provided in the JSON as a string of a decimal number. For example

```javascript
  {
    "Type": "uint32",
    "Value": "25"
  }
```

* `uint64` - Integer with 64 bit precision. Matches the `uint64` type in Go contracts. Provided in the JSON as a string of a decimal number. For example

```javascript
  {
    "Type": "uint64",
    "Value": "10029999"
  }
```

* `string` - String. Matches the `string` type in Go contracts. Provided in the JSON as a UTF8 string. For example

```javascript
  {
    "Type": "string",
    "Value": "Hello world"
  }
```

* `bytes` - An array of bytes \(blob\). Matches the `[]byte` type in Go contracts. Provided in the JSON as a hex string. For example

```javascript
  {
    "Type": "bytes",
    "Value": "0x00ff018e00ab2fe901"
  }
```

* `bool` - boolean value. Matches the `bool` type in Go contracts. Provided in the JSON as a string with value `"0"` or `"1"`. For example

```javascript
  {
    "Type": "bool",
    "Value": "1"
  }
```

* `uint256` - Integer with 256 bit precision. Matches the `*big.Int` type in Go contracts. Provided in the JSON as a hex string with fixed size of 64 hexes. For example

```javascript
  {
    "Type": "uint256",
    "Value": "0x00112233445566778899aabbccddeeff00112233445566778899aabbccddeeff"
  }
```

* `bytes20` - A fixed size array of 20 bytes. Matches the `[20]byte` type in Go contracts. Provided in the JSON as a hex string with fixed size of 40 hexes. For example

```javascript
  {
    "Type": "bytes20",
    "Value": "0x0011223344556677889900112233445566778899"
  }
```

* `bytes32` - A fixed size array of 32 bytes. Matches the `[32]byte` type in Go contracts. Provided in the JSON as a hex string with fixed size of 64 hexes. For example

```javascript
  {
    "Type": "bytes32",
    "Value": "0x00112233445566778899aabbccddeeff00112233445566778899aabbccddeeff"
  }
```

All the slice of these types are also supported. The type has the suffix 'Array' and the value is JSON Array of strings representing the values. For example

```javascript
  {
    "Type": "uint64Array",
    "Value": [
      "10029999",
      "1997",
      "12345678"
    ]
  },
  {
    "Type": "bytes20Array",
    "Value": [
      "0x0011223344556677889900112233445566778899",
      "0x0000000000000000000000111111111111111111"
    ]
  }
```

In addition to these primitives, Gamma CLI supports several aliases for convenience:

* `gamma:keys-file-address` - An account address by ID. The value should be an account ID from `orbs-test-keys.json`. An alias for the type `bytes` which means it matches the `[]byte` type in Go contracts. Used to pass the account address in raw form.

```javascript
  {
    "Type": "gamma:keys-file-address",
    "Value": "user3"
  }
```

## Overriding arguments from command line

Consider a JSON for a typical **transfer** method

{% code title="transfer-15.json" %}
```javascript
{
  "ContractName": "MyToken",
  "MethodName": "transfer",

  "Arguments": [
    {
      "Type": "uint64",
      "Value": "15"
    },
    {
      "Type": "bytes",
      "Value": "b3d1caa2b3680e2c8feffa269c207c553fbbc828"
    }
  ]
}
```
{% endcode %}

The first argument is the **amount** and the second argument is the **recipient address**.

If you want to send multiple transactions with different amounts or different addresses, creating multiple JSON files containing the different values can be a hassle.

Instead, use the optional `-arg1` and `-arg2` command line arguments to override values

```text
gamma-cli send-tx transfer-15.json
```

           will send **15** tokens to recipient **b3d1caa2b3680e2c8feffa269c207c553fbbc828**

```text
gamma-cli send-tx transfer-15.json -arg1 22
```

           will send **22** tokens to recipient **b3d1caa2b3680e2c8feffa269c207c553fbbc828**

```text
gamma-cli send-tx transfer-15.json -arg2 7ccd7f7c18c0cb749dd8b8949f4b4e31f7188394
```

           will send **15** tokens to recipient **7ccd7f7c18c0cb749dd8b8949f4b4e31f7188394**

When the type is an Array \(slice\) should be a STRINGIFIED JSON representation for example if the type is a boolArray the override value can be something like this :

"\[\"0\", \"1\", \"1\"\] - this is a string representation of `[]bool{false, true, true}`

