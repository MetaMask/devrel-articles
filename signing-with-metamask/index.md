## Introduction

Signing is an act that carries a big responsibility. You sign things like contracts, cheques, and legal documents. If you create an application for signing things, chances are that any mediumly tech-savvy person will be able to use it. But in the blockchain world, what does signing mean?

This question you should take lightly, especially when it comes to your users and presenting them with transactions, messages, and data to be signed. Establishing trust with your users is critical and will be the tutorial's focus. In the following few paragraphs, we will put our dual UX and blockchain hats on and sign a message with Metamask.


## Signing a message

First, Let's demystify what signing means in the world of crypto. In the physical world, your identity is proven with an identification card or, in some contexts, a written signature. This validity is typically ensured because they are verified by a trusted entity such as a notary or a governmental organization.

Trust in a blockchain comes from nodes in the network agreeing on the validity of transactions between two parties. It is to these transactions that the term signing is most often applied. Signing a transaction on Ethereum means using a private key to authorize a transfer of Ether or interaction with a smart contract on the Ethereum blockchain. It proves the ownership of the Ethereum address associated with the private key and allows the transaction to be added to the blockchain.

But signing goes beyond this. It can also be used for other purposes. For example, signing a message can be used to proven to come from a specific address. This is useful for many use cases like authentication, authorizations, and even exchanges of information. MetaMask, a fully featured wallet, can be used to sign messages and data. We will see popular methods and even explore cutting-edge Dapp architectures built on top of it.

## Signing a message with MetaMask

MetaMask always does its best to make sure standards are followed and that the user is in control of their information. The methods we'll discuss today are the ones we recommend to be implemented by Dapps. We'll discuss signing simple messages and signing typed data. The respective methods are `eth_sign` and `eth_signTypedData` and can be submitted through the `window.ethereum.request` JSON-RPC API. 

### Signing a simple message

In some cases, if you want to have users approve or sign a message and don't intend to use the message on a chain, you can use the `personnal_sign` method,  defined in [EIP-191](https://eips.ethereum.org/EIPS/eip-191). This method is also relatively simple to implement in your code:

```ts
// the message to be signed
const message = 'I like tacos and I approved of this message'
const from = '0x...' //* pass in the user's address here
window.ethereum.request({
      method: 'personal_sign',
      params: [mesasge, from],
})
```

The advantage of this method is by far its simplicity and readability for users; they will be prompted by the MetaMask extension and will have a similar user experience to signing a document or a simple contract. A well-known use case is "Sign In With Ethereum," abbreviated as SIWE, defined in  [EIP-4361](https://eips.ethereum.org/EIPS/eip-4361), where users approve connecting to an application and this signature is validated before a session is created in the server.

Even if we see that 95% of users typically will approve a request for signature, one of the limits with `personnal_sign` is around using it inside smart contracts. While we can use the `string` value of the message inside a smart contract, a string is expensive to parse into more complicated data formats.

This is where `eth_signTypedData_v4` comes in!

### Signing typed data.

JSON or JavaScript Object Notation is a famous data format used in web applications. However, JSON support is limited in the world of smart contracts, where performance means increasing user costs. Luckily [EIP-712](https://eips.ethereum.org/EIPS/eip-712) is a proposed standard that allows users to sign data that smart contracts can understand. 

Its usage is fairly similar to `personal_sign`, instead you simply have to pass a request of type `eth_signTypedData_v4` and specify the Solidity types and details about the smart contract verifying the message:

```ts
// The message will be parsed in 
const message = JSON.stringify({
    domain: {
      chainId,
      name: "Example App",
      verifyingContract: "0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC",
      version: "1",
    },
    // should implement the top level type
    message: {
      prompt: "Are Doritos tacos any good?",
      answer: `YES THEY ARE!`,
    },
    // Top level type
    primaryType: 'QA',
    types: {
      EIP712Domain: [
        { name: 'name', type: 'string' },
        { name: 'version', type: 'string' },
        { name: 'chainId', type: 'uint256' },
        { name: 'verifyingContract', type: 'address' },
      ],
     // defining the top level type here. types refer to Solidity types    
      QA: [
        { name: 'prompt', type: 'string' },
        { name: 'answer', type: 'string' },
      ],
    },
  });
const from = '0x...' 
window.ethereum.request({ 
    method: 'eth_signTypedData_v4',
     params: [from, message]
})
```

The lift for front-end developers is a bit higher, but the most significant advantage of this signing method is that it opens up a world of possibilities for smart contracts! It also helps that we witness upwards of 97% approval of these messages in MetaMask! Now let's explore what kind of robust architectures you can unlock with `eth_signTypedData_v4`

### A New Generation of Dapps!

In a world where malicious actors abound, moving approvals on-chain has a considerable amount of benefits:

- auditable code 
- ability to create authorization layers that live on-chain directly without requiring user approvals on each action.

The last benefit is one I want to explore more. Since typed data is easy to understand for smart contracts, we can use it to hold long-lived user approvals on-chain. Take this example, a smart-contract implementing a paycheck every two weeks. The steps would happen as follows:

1. An employer deposits a 10,000$ amount in a smart contract for the next ten weeks of paychecks
1. The employer signs an authorization using `eth_signTypedData_v4` that approves 1000$ per week for an employee
1. The employee, on his own, will claim the salary each week
1. The smart contract will verify if the authorization is valid and allow the disbursement
1. The employer can revoke his authorization at any time if they terminate the contract

This kind of scenario is the user experience you can implement if you integrate `eth_signTypedData_v4`. It would help if you worked towards a user interface that communicates what happens and educates users about your smart contract when implementing such an authorization layer.

## Conclusion

We saw a lot of advanced concepts today, but understanding signatures is a great way to build sustainable and user-friendly Dapps. After the initial learning curve of communicating between wallet, smart contracts, and users, we are empowered to make better, more sustainable apps.