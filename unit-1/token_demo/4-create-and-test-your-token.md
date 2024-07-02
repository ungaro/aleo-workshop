# 4. Create and Test Your Token

Here we will create a token program of our own.

## Create a Token Contract

For this demo, our desired features are following:

- **Mint Function:** Able to mint a specific `amount` of `token` to the one who called the mint function.
- **Transfer Function**: Able to transfer a specific `amount` of the `token` that was minted using the mint function to another user (`recipient`).

### **Step One: Define Your Token Record**

Define a token struct with an owner and balance:

```
record Token {

    // The token owner, any record must be defined with the `owner` field.

    owner: address,

    // Token balance of the user.

    balance: u32,

}
```

### **Step Two: Define the Mint Function**

Define a mint transition that takes a balance and returns a token record:

```
transition mint(amount: u32) -> Token {

    return Token {

        owner: self.caller,

        balance: amount,

    };

}
```

### **Step Three: Define the Transfer Function**

Define a transfer transition that takes a receiver, amount, and token, and returns two token records:

```
transition transfer(receiver: address, transfer_amount: u32, input: Token) -> (Token, Token) {

    let sender_balance: u32 = input.balance - transfer_amount;

    let recipient: Token = Token {

        owner: receiver,

        balance: transfer_amount,

    };



    let sender: Token = Token {

        owner: self.caller,

        balance: sender_balance,

    };



    return (recipient, sender);

}
}
```

### **Final Step: Overview of Your main.leo File**

This is what your `main.leo` file should look like:

```program [your_token_name].aleo {

// Step one: define your token record

record Token {

    // The token owner, any record must be defined with the `owner` field.

    owner: address,

    // Token balance of the user.

    balance: u32,

}



// Step two: define mint function

transition mint(amount: u32) -> Token {

    return Token {

        owner: self.caller,

        balance: amount,

    };

}



// Step three: define transfer function

transition transfer(receiver: address, transfer_amount: u32, input: Token) -> (Token, Token) {

    let sender_balance: u32 = input.balance - transfer_amount;

    let recipient: Token = Token {

        owner: receiver,

        balance: transfer_amount,

    };



    let sender: Token = Token {

        owner: self.caller,

        balance: sender_balance,

    };



    return (recipient, sender);

}

}
```

## Test Program

### Test Mint function

1. **Build Leo:**

```bash
leo build
```

1. **Ensure you see:**

```
Leo ✅ Compiled '[your_token_name].aleo' into Aleo instructions
```

2. **First Test Mint Function:**

```
leo run mint 100u32
```

3. **Ensure you see:**

```bash
Leo ✅ Compiled '[your_token_name].aleo' into Aleo instructions



⛓  Constraints



 • '[your_token_name].aleo/mint' - 2,020 constraints (called 1 time)



➡️  Output



 • {

  owner: [number].private,

  balance: 100u32.private,

  _nonce: [number]group.public

}
```

4. The output should be a record of 100 new tokens.

### Test Transfer function

Then, test the transfer function to transfer 10 tokens to another address.

1. **Run the Transfer Command:**

```bash
leo run transfer <recipient's address> 10u32 "<Token Record>"
```

2. **Example:**

```bash
leo run transfer aleo1qqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqq9d 10u32 "{ owner: aleo1abcdefgh..., balance: 100u32.private }"
```

3. **Expected Output:** The output should show two records: one where 10 tokens are owned by the recipient, and the remaining 90 tokens are owned by the original owner.

```bash
{
  "recipient": {
    "owner": "aleo1xyz...",
    "balance": 10u32.private
  },
  "sender": {
    "owner": "aleo1...",
    "balance": 90u32.private
  }
}
```

Notes:

- Remember to replace` <recipient's address>` with the actual address of the recipient.
- The input token record should be the one returned after you minted.
- The record logged in the terminal usually has .private and .public keywords after all properties of the record. These are just indicators to show whether certain properties of the record are public or private.
