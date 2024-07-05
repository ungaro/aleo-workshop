# 4. Create and Test Your Token

Here we will create a token program of our own.

## Create a Token Contract

For this demo, our desired features are following:

- **Mint Function:** Able to mint a specific `amount` of `token` to the one who called the mint function.
- **Transfer Function**: Able to transfer a specific `amount` of the `token` that was minted using the mint function to another user (`recipient`).

### **Step One: Define Your Token Record**

Define a token struct with an owner and balance:

```
program token_jimito.aleo {
    // Step one: define your token record
    record Token {
        // The token owner, any record must be defined with the `owner` field.
        owner: address,
        // Token balance of the user.
        balance: u64,
    }
```

### **Step Two: Define the Mint Function**

Define a mint transition that takes a balance and returns a token record:

```
    // Step two: define mint function
    transition mint(amount: u64) -> Token {
        return Token {
            owner: self.caller,
            balance: amount,
        };
    }
```

### **Step Three: Define the Transfer Function**

Define a transfer transition that takes a receiver, amount, and token, and returns two token records:

```
    // Step three: define the transfer function
    transition transfer(token: Token, to: address, amount: u64) -> (Token, Token) {
        // Checks the given token record has sufficient balance.
        // This `sub` operation is safe, and the proof will fail
        // if an overflow occurs.
        // `difference` holds the change amount to be returned to the sender.
        let difference: u64 = token.balance - amount;

        // Produce a token record with the change amount for the sender.
        let remaining: Token = Token {
            owner: token.owner,
            balance: difference,
        };

        // Produce a token record for the specified receiver.
        let transferred: Token = Token {
            owner: to,
            balance: amount,
        };

        // Output the sender's change record and the receiver's record.
        return (remaining, transferred);
    }
```

### **Final Step: Overview of Your main.leo File**

This is what your `main.leo` file should look like:

```
program token_jimito.aleo {
    // Step one: define your token record
    record Token {
        // The token owner, any record must be defined with the `owner` field.
        owner: address,
        // Token balance of the user.
        balance: u64,
    }

    // Step two: define the mint function
    transition mint(amount: u64) -> Token {
        return Token {
            owner: self.caller,
            balance: amount,
        };
    }

    // Step three: define the transfer function
    transition transfer(token: Token, to: address, amount: u64) -> (Token, Token) {
        // Checks the given token record has sufficient balance.
        // This `sub` operation is safe, and the proof will fail
        // if an overflow occurs.
        // `difference` holds the change amount to be returned to the sender.
        let difference: u64 = token.balance - amount;

        // Produce a token record with the change amount for the sender.
        let remaining: Token = Token {
            owner: token.owner,
            balance: difference,
        };

        // Produce a token record for the specified receiver.
        let transferred: Token = Token {
            owner: to,
            balance: amount,
        };

        // Output the sender's change record and the receiver's record.
        return (remaining, transferred);
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
leo run mint 100u64
```

3. **Ensure you see:**

```bash
Leo ✅ Compiled '[your_token_name].aleo' into Aleo instructions
⛓  Constraints
 • '[your_token_name].aleo/mint' - 2,020 constraints (called 1 time)
➡️  Output
 • {
  owner: [number].private,
  balance: 100u64.private,
  _nonce: [number]group.public
}
```

4. The output should be a record of 100 new tokens.
```bash
➜  token_jimito leo run mint 100u64
       Leo ✅ Compiled 'token_jimito.aleo' into Aleo instructions

⛓  Constraints

 •  'token_jimito.aleo/mint' - 2,020 constraints (called 1 time)

➡️  Output

 • {
  owner: aleo16l94q9mrfvwddz7mtsla9dsnr6usr580p3tuqu27hff8sfrgcs9s3un3xw.private,
  balance: 100u64.private,
  _nonce: 7866491247063862570923315683237265939712826472158406110725485131341638718073group.public
}

       Leo ✅ Finished 'token_jimito.aleo/mint'
```

### Test Transfer function

Then, test the transfer function to transfer 25 tokens to another address.

1. **Run the Transfer Command:**

```
leo run transfer <recipient's address> 100u64 "<Token Record>"
// You can create a new test wallet using `leo new account`
```

2. **Example:**

```
leo run transfer "{
  owner: aleo1qlw77yxvh0lhzzqxs04yva5uguksfnvtvhknv0taft02tqztyg8qtetkxv.private,
  balance: 1500u64.private,
  _nonce: 639032693423754082364536775069039453230324007423924798412607788930508840691group.public
}" aleo19wt5nknak444l0s6raf4h7nsx63j597y6pk3urhc79f43g7u7srsupyqdu 100u64
```

3. **Expected Output:** The output should show two records: one where 25 tokens are owned by the recipient, and the remaining 90 tokens are owned by the original owner.

```
token_jimito leo run transfer "{
  owner: aleo16l94q9mrfvwddz7mtsla9dsnr6usr580p3tuqu27hff8sfrgcs9s3un3xw.private,
  balance: 100u64.private,
  _nonce: 7866491247063862570923315683237265939712826472158406110725485131341638718073group.public
}" aleo19wt5nknak444l0s6raf4h7nsx63j597y6pk3urhc79f43g7u7srsupyqdu 25u64
       Leo ✅ Compiled 'token_jimito.aleo' into Aleo instructions

⛓  Constraints

 •  'token_jimito.aleo/transfer' - 4,107 constraints (called 1 time)

➡️  Outputs

 • {
  owner: aleo16l94q9mrfvwddz7mtsla9dsnr6usr580p3tuqu27hff8sfrgcs9s3un3xw.private,
  balance: 75u64.private,
  _nonce: 5564054047223494909855000267617287724552224897560459512189989388250299122119group.public
}
 • {
  owner: aleo19wt5nknak444l0s6raf4h7nsx63j597y6pk3urhc79f43g7u7srsupyqdu.private,
  balance: 25u64.private,
  _nonce: 1091633311462665956519582503768472411527844165155556863751507107350855060704group.public
}

       Leo ✅ Finished 'token_jimito.aleo/transfer'
```

Notes:

- Remember to replace` <recipient's address>` with the actual address of the recipient.
- The input token record should be the one returned after you minted.
- The record logged in the terminal usually has .private and .public keywords after all properties of the record. These are just indicators to show whether certain properties of the record are public or private.
