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

## Function Types

- `transition`: Used for off-chain computation. Describes the change of a record’s state.
- `finalize`: Used for on-chain computation. Runs immediately after the transition function execution off-chain. When declaring it in a Leo program, it must immediately follow a transition function and have the same name.
- `function`: Helper functions that can only be called within transition, finalize, or other helper functions.
- `inline`: Functions that can only be called within transition, finalize, helper, or other inline functions.
