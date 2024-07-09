# 3. Basic Data Types and Functions

We won’t cover all of the preliminaries of the `leo` language, but we’ll cover the most essential ones for this workshop.

This section serves as a cheat sheet of basic data types and functions that we will use to get started. For more detailed information about the Leo language, we recommend checking out the original developer documentation [here](https://developer.aleo.org/leo/language).

## Basic Data Types

- `bool`: Represents a boolean value, either `true` or `false`.
- `i8`, `i16`, `i32`, `i64`: Signed integers of different sizes.
- `u8`, `u16`, `u32`, `u64`: Unassigned integers of different sizes.
- `address`: Type for wallet addresses/public addresses.
- **Array**: Type for static arrays. Arrays are declared as[type; length] aand can be nested. Arrays cannot be empty or modified.
- `mapping`:  A mapping is declared as mapping {name}: `{key-type} => {value-type}`. Mappings contain key-value pairs and are stored on-chain.
- `record`: A record data type is declared as record {name} {}. Records contain component declarations `{visibility} {name}: {type}`. Record data structures must contain the `owner` component

# Additional Detail

1. bool: Represents a boolean value, either true or false.
	•	Example: let is_active: bool = true;
2.	Signed Integers (i8, i16, i32, i64):
	•	Signed integers can store both positive and negative values.
	•	i8: 8-bit signed integer, range: -128 to 127.
	•	i16: 16-bit signed integer, range: -32,768 to 32,767.
	•	i32: 32-bit signed integer, range: -2,147,483,648 to 2,147,483,647.
	•	i64: 64-bit signed integer, range: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.
	•	Example: let small_number: i8 = -5;
3.	Unsigned Integers (u8, u16, u32, u64):
	•	Unsigned integers can only store non-negative values.
	•	u8: 8-bit unsigned integer, range: 0 to 255.
	•	u16: 16-bit unsigned integer, range: 0 to 65,535.
	•	u32: 32-bit unsigned integer, range: 0 to 4,294,967,295.
	•	u64: 64-bit unsigned integer, range: 0 to 18,446,744,073,709,551,615.
	•	Example: let age: u8 = 30;
4.	address: Type for wallet addresses/public addresses used in blockchain transactions.
	•	Example: let user_address: address = "aleo1...";
5.	Array: Type for static arrays. Arrays are declared as [type; length] and can be nested. Arrays cannot be empty or modified.
	•	Example: let numbers: [u8; 3] = [1, 2, 3];
6.	mapping: A mapping is declared as mapping {name}: {key-type} => {value-type}. Mappings contain key-value pairs and are stored on-chain.
	•	Example: mapping balances: address => u64;
7.	record: A record data type is declared as record {name} {}. Records contain component declarations {visibility} {name}: {type}. Record data structures must contain the owner component.
	•	Example:
``` bash
record Token {
    owner: address,
    amount: u64,
}
```
## Function Types

- `transition`: Used for off-chain computation. Describes the change of a record’s state.
- `finalize`: Used for on-chain computation. Runs immediately after the transition function execution off-chain. When declaring it in a Leo program, it must immediately follow a transition function and have the same name.
- `function`: Helper functions that can only be called within transition, finalize, or other helper functions.
- `inline`: Functions that can only be called within transition, finalize, helper, or other inline functions.
