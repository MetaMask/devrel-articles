## Introduction

“Security and reliability are the backbone of any successful online transaction”. 

The above statement cannot be overemphasized enough. 

Blockchain technology has brought about a paradigm shift in this regard, providing unparalleled levels of security and transparency. This is not to say there hasn’t or will not be bad actors trying to “game” the system. Afterall, as with any new technology, there are bound to be certain complexities and challenges. One such complexity is the process of signing data with MetaMask.

For many, the technical jargon and complex algorithms associated with digital signatures and MetaMask can be overwhelming. But what if I told you that understanding and utilizing this technology can be simple and straightforward?

In this article, I will cover the fundamental concepts of digital signatures and the role they play in securing and signing online transactions, then delve into the process of signing data with MetaMask, examining how it utilises digital signatures to protect your digital assets. I'll also provide practical examples of how to use the different methods of signing data. so you can apply your newfound knowledge with confidence. 

The goal of this post is to clear out the difference between signing a transaction and generally signing messages by covering all aspects, right from the basics, in a way that is easily understandable, so you can take control of your digital assets in the most secure and efficient way possible. 
This article is for anyone who is interested in blockchain technology, developers, business owners and individuals who are looking to secure their digital assets. 

> But first..what is a digital signature and data signing in web3?

A digital signature is a mathematical mechanism that is used to verify the authenticity and integrity of digital data, and signing data in web3 refers to the process of using digital signatures to authenticate and authorize transactions on the blockchain. It works by combining a user's private key, which is kept secret, with the data to be signed, and then encrypting it using a one-way hash function. The resulting signature can be verified by anyone with access to the user's public key and the original data.

Digital signatures are used to sign transactions in web3 before they are broadcasted to the blockchain network. This ensures that only the authorized user can initiate a transaction and that the transaction has not been tampered with in transit. 

Signing data is also used in smart contracts, in order to prove that a user has the necessary permissions to execute a certain function or to transfer a specific asset. Digital signatures are a fundamental aspect of web3 and are crucial for maintaining the security and integrity of the blockchain network.

> And what does MetaMask have to do with all of this?

MetaMask is a popular browser extension that allows users to access the Ethereum blockchain and interact with decentralized applications (dApps) and Signing data with MetaMask is a feature that allows users to sign digital data with their Ethereum private key, providing a way to prove ownership of an Ethereum address. What this means is that they are effectively proving to the network that they are the owner of the account and that they have the authority to transfer the specified assets.
When you sign data with MetaMask, your private key never leaves your device. This means that your private key is safe from hackers and other malicious actors who might try to steal it. Additionally, MetaMask uses a technique known as "hashing" to ensure that your data is secure and cannot be tampered with.

Below are some of the key milestones in the journey of signing data and transactions with MetaMask:

2016: MetaMask was first released as a browser extension for Google Chrome, allowing users to interact with the Ethereum blockchain and sign transactions with their private key.
2017: MetaMask added support for signing data and messages, allowing users to prove ownership of an Ethereum address.
2018: MetaMask introduced the ability to sign typed data, which is a specific format for structured data specified by the EIP-712 standard. This feature enabled users to sign more structured and organized data.
2019: MetaMask introduced the ability to sign and send transactions directly from the browser extension, eliminating the need for users to copy and paste the transaction data into a separate signing tool.
2020: MetaMask introduced the ability to sign transactions using hardware wallets, such as Trezor and Ledger, providing an additional layer of security for users.
2021: MetaMask introduced the ability to sign messages using a new, more secure method called the "Ethereum Message Signing Protocol (EMSP)".
Throughout its journey, MetaMask has continued to evolve and improve, providing users with more secure and user-friendly ways to sign data and transactions on the Ethereum blockchain. With the latest updates, MetaMask is now one of the most popular tools for signing data and transactions on the Ethereum network, and it is widely used by developers and users alike.

ethers.js played a role in the journey of signing data and transactions with MetaMask by providing an alternative approach to signing data and transactions on the Ethereum blockchain. It offers a developer-friendly API and better support for TypeScript, which makes it easier for developers to build dApps and interact with the Ethereum blockchain.

While MetaMask has been focused on providing a user-friendly interface for signing data and transactions, ethers.js( an alternative to web3.js and a JavaScript library for interacting with the Ethereum blockchain) has been focused on providing a developer-friendly library for building dApps and interacting with the Ethereum blockchain. ethers.js has been widely adopted by developers as a more intuitive and easy-to-use library for signing data and transactions.

MetaMask and ethers.js are not mutually exclusive and can be used together, in fact, developers can use MetaMask to interact with the Ethereum blockchain and sign data and transactions, and use ethers.js to build their dApp's front-end. ethers.js may also be used to sign data and transactions on other Ethereum clients such as Geth or Parity.

## Methods of Signing Data With MetaMask

We’ll explore various ways of signing data using the provider injected by MetaMask as well as implementations in web3.js and wthers.js:
eth_sign: This method is used to sign data with the Ethereum address's private key, and returns the signature in the format of `"0x<r><s><v>"`.

This method is mainly used to sign data and prove ownership of an Ethereum address.  However, a limitation of this method is that it does not include any kind of prefix before signing the data, which could lead to the signature not being recognized as valid by some smart contracts. It also poses a security risk so it should be avoided.


personal_sign: This method is similar to `eth_sign` but it adds an "Ethereum Signed Message" prefix to the data before signing it. It is part of the JSON-RPC personal module, which is for personal account management. It signs data with a user's private key and returns the signature. This method is used to sign data and prove ownership of an Ethereum address.

```tsx
window.ethereum.request({ method: 'personal_sign',  params: [msg, from],  });
```

where `data` is the data to be signed, `address` is the address of the user signing the data and `callback` is an optional callback function to handle the result. Advantages of this method include the added security provided by the prefix, which allows the signature to be recognized as valid by more smart contracts. However, a limitation of this method is that it only supports UTF-8 encoded data. Developers should choose this method if they need to sign data that will be recognized as valid by more smart contracts and the data is UTF-8 encoded.



eth_signTypedDataV4: This method is used to sign typed data, which is a specific format for structured data specified by the EIP-712 standard, and returns the signature in the format of `0x<r><s><v>`. This method is mainly used to sign data and prove ownership of an Ethereum address. 

```tsx
window.ethereum.request({ method: 'eth_signTypedData_v4', params: [address, data] })
```

where `data` is the typed data object to be signed, `address` is the address of the user signing the data, and `callback` is an optional callback function to handle the result.  Advantages of this method include its support for typed data, which allows for more structured and organised data, and its support for the EIP-712 standard, which is widely recognized and supported by the Ethereum community. However, a limitation of this method is that it only supports typed data, which means it can't be used to sign any kind of data. Developers should choose this method if they need to sign typed data according to the EIP-712 standard.

When using these methods, it's important to keep in mind that the user's private key must be kept safe and secure. It's also important to validate the data before signing it, and to use a secure connection to prevent man-in-the-middle attacks.


## What do users prefer?

An interesting metric to consider is how often will users accept a signature request when a Dapp presents it to them. This is a good indicator of how much trust users have in the Dapp and how much they trust the signature request. Here is our of conversion rates for the different signature methods:

- eth_sign is accepted by 56% of users
- personal_sign is accepted by 95%
- signTypedData_v4 is accepted by 97%




## Conclusion

MetaMask allows users to sign data in several ways, each method has its own specific use case, developers should choose the method that fits their use case best, whether it's signing data to prove ownership of an Ethereum address or signing transactions to be sent to the Ethereum network. 

It's important to keep in mind the security and user experience, as well as to validate the data and use a secure connection to prevent man-in-the-middle attacks. By following best practices and implementing the appropriate method, developers can ensure the integrity and authenticity of the data signed using MetaMask. It's also important to note that, in order to use these methods, the user must have MetaMask installed and configured on their browser and have granted the dApp permission to access their MetaMask account.

MetaMask provides several methods for signing data and transactions, each method has its own specific use case and developers should choose the appropriate method for their use case. To ensure the security and integrity of the data, developers should also follow best practices, which in our opinion is to use `signedTypeDataV4` as a default and revert to `personal_sing` in edge cases. Remeber to implement appropriate measures to validate the data, use a secure connection and test the code thoroughly before deploying it to production.





