# Introduction

Everywhere you go, you have a digital identity. This identity is the collection of data that represents your activity online. It is difficult to stay truly anonymous online in this era of social media.
If you are present on a social like Facebook or TikTok, you probably have seen disturbing advertisements after visiting a website seemingly unrelated to those platforms. This is because websites implement a variety of cross-site tracking technologies, identifying you across the Internet.

## An Overview of Digital Identity In Present Day Earth, 2023

The term “Digital identity” refers to the concept of a person or entity's identity existing in the digital world. It encompasses the information, attributes, and characteristics that are associated with a person or entity, and it can be used for a wide range of purposes such as authentication, authorization, and access control. In tech jargon, a digital identity is an online or networked identity adopted or claimed in cyberspace by an individual, organization or electronic device.

Digital identities can be centralized or decentralized, depending on how they are created and managed. Centralized digital identities are controlled by a single entity, such as a government or a corporation, while decentralized digital identities are controlled by the individual or entity they represent.

A digital identity can the following simple attributes such as a user’s:

- Name
- Address
- Username and password
- Date of birth

Or complex attributes such as a user’s:

- Online search activities, like electronic transactions
- Social security number
- Medical history
- Purchasing history or behavior
- Biometric data
- Digital certificates

Use cases for digital identities are seen in various industries such as finance, healthcare, and e-commerce, and for various uses such as online banking, secure messaging, and personal data management.

A widespread issue plaguing digital identity on the internet is Identity theft, so the subject of digital identity authentication and validation measures are critical to ensuring Web and network infrastructure security in the public and private sectors. Admittedly, there has been a lot of talk about authentication, and with the advent of blockchain technology, digital identities are also being used in decentralized applications and platforms that are built on the blockchain. In the recent past, the Web3 community has been fragmented around multiple wallets and authentication methods.

Web3 developers are digital self-sovereignty advocates so let’s look at what the concept of digital identity means in web3

## Identity In Web3 and its implementation

Identity in web3 refers to the concept of self-sovereign identity, which allows individuals to own and control their own digital identity. In traditional web2 systems, identities are often controlled by centralized entities such as governments and corporations, but in web3, individuals have the ability to create and manage their own digital identities using blockchain technology.

There are several methods of implementing identity in web3 with popular ones such as Decentralized Identity Protocols(DID) and Smart Contract-based Identity Protocols, and others like Self-sovereign identity (SSI) systems, Public Key Infrastructure (PKI) based systems and Biometric-based Identity as well.

1. Decentralized Identity (DID) protocols: These protocols provide a way for users to create and manage their own digital identities on the blockchain. DIDs are unique identifiers that are registered on a blockchain and can be used to authenticate and authorize individuals on the web3 network. They can also be used to link different identities, such as social media and email, to a single blockchain-based identity.

2. Smart Contract-based Identity Protocols: These protocols use smart contracts to store and manage user identities on the blockchain. Users can create and manage their identities using smart contracts, which can also be used to authenticate and authorize users on web3 applications.

3. Self-sovereign identity (SSI) systems: They are based on the same principles of DIDs, but they allow the user to hold and control their own identity data, with out the need of a centralized entity.

4. Public Key Infrastructure (PKI) based systems: They use digital certificates and public and private keys to authenticate and authorize users on web3 applications, similar to how PKI is used in traditional web2 systems.

5. Biometric-based Identity: Biometrics such as fingerprints, facial recognition, and voice recognition can be used to create and authenticate digital identities on web3.

With web3, individuals have more control over their personal data and identity, allowing them to share it selectively, and giving them the ability to revoke access to it at any time. Additionally, it also allows to have multiple identities, and connect them together in a way that they can be used to prove the identity of the user. It is pertinent to remember, that the implementation of some of these methods are still in the early stages and there are still ongoing research and development to make them more user-friendly and widely adopted.

Blockchain developers have long talked about developing “decentralized” identity standards to save users from the dangers of Big Login, and this birthed: Sign-in With Ethereum proposal, a digital identity standard which was built by the community with direct support from the Ethereum Foundation and ENS, with Spruce Systems tapped to lead the charge.

## Sign In With Ethereum proposal and how it affects digital identity

The Sign In With Ethereum(SIWE) proposal was a proposed standard for using Ethereum to authenticate and authorize users on web3 applications. It aimed to provide a standard way for users to sign in to web3 applications using their Ethereum address and private key, similar to how users currently sign in to web2 applications using their email and password. It is a process of using a private key to authenticate a user's identity on the Ethereum blockchain. A private key is a unique string of characters that is associated with an Ethereum address, and it is used to sign digital transactions. When a user signs in with Ethereum, they are providing a digital signature using their private key to prove that they are the owner of the associated Ethereum address. This allows them to access their account and perform actions such as sending and receiving Ether, interacting with smart contracts, and more.

With SIWE, users would create an Ethereum address and private key specifically for signing in to web3 applications. When they want to sign in to a web3 application, they would use their private key to sign a message that proves they are the owner of the associated Ethereum address. The web3 application would then verify the signature and authenticate the user.
SIWE affects digital identity by

Allowing individuals to use their Ethereum address and private key as a decentralized and self-sovereign way to authenticate and authorize themselves on web3 applications.
Eliminating the need for users to create and remember separate login credentials for each web3 application they use.
Allowing users to use their Ethereum address as a decentralized identity across different web3 applications.
Enabling web3 applications to authenticate and authorize users without the need for centralized identity providers, such as social media login or email and password, which could lead to more privacy and security for the user.

The idea behind the proposal is to standardize the way you authenticate with a digital identity. The following steps are followed:

A server creates a unique number called a Nonce for each user that will sign-in.
A user requests to connect a site with their wallet.
The user is presented with a unique message that indicates the Nonce and information about the website.
The user signs in with their wallet.
The user is then authenticated and the website is given access to data about the user that was approved.

Metamask is a popular tool and a browser extension that allows users to interact with the Ethereum blockchain and can be used to implement digital identity and SIWE. Metamask can be used to create and manage Ethereum addresses, which can be used as a digital identity on web3 platforms and dApps.

For your users the experience is simple but there are multiple steps that are happening behind the scenes.

## How to implement Sign In With Ethereum

As mentioned above, we will need to generate a unique number called a Nonce, since this should be done on a server, we will be working with Next.js, the most popular React framework for building server-side rendered applications.

We will starting from a basic Next.js application created with [`create-next-app`](create-next-app) and we will use the following
libraries:

- [`@metamask/providers`](https://www.npmjs.com/package/@metamask/providers) - A library for interacting containing TypeScript types for the MetaMask provider API.
- [`ethers`](https://www.npmjs.com/package/ethers) - A library containing different utilities for interacting with the Ethereum blockchain.
- [`siwe`](https://www.npmjs.com/package/siwe) - A library containing utilities for implementing Sign In With Ethereum.
- [`iron-session`](https://www.npmjs.com/package/iron-session) - A library for implementing session management in Next.js applications.

**N.B. The full code is [available here](https://github.com/MetaMask/examples/tree/main/examples/metamask-siwe).**

### A dance between the client and the server

With these libraries in place, we can lay down the architecture for implementing SIWE. In order to connect users we will to implement the following:

1. Generate a Nonce inside `getServerSideProps`.
2. Pass the Nonce to the client
3. Connect to a users wallet
4. Make the user sign a message containing the nonce
5. Verify the signature
6. Store the signature in a session

###  Generate a Nonce inside `getServerSideProps`

Our first step is to generate a Nonce inside `getServerSideProps` of our login page which is located at `pages/login.tsx`.

Generating the Nonce inside `getServerSideProps` is important because it will be executed on the server, and we will be able to pass it to the client. This is faster than fetching it from an API route like in other implementation

```tsx
export const getServerSideProps = () => {
  const nonce = generateNonce();

  return {
    props: {
      nonce,
    },
  };
};

With this, we can now pass the nonce to the client.
```

###  Pass the Nonce to the client


Next, we will pass the Nonce to the client. This will happen by defining a default export for the login page which will be a React component that will receive the nonce as a prop.

```tsx
type Props = { nonce: string }

export default function Login({ nonce }: Props) {
    // ...rest of the component
```

###  Connect to a users wallet and sign a message

Now we go to the core of our implementation, connecting to a users wallet. This will happen inside the `connect` function which will be called when the user clicks the connect button.

__[See the full function](https://github.com/MetaMask/examples/tree/main/examples/metamask-siwe/pages/login.tsx)__

Our function will work as follows:

1. Request the user to connect to their wallet with `window.ethereum.request({ method: 'eth_requestAccounts' })`
2. Grab the current network with `window.ethereum.request({ method: 'eth_chainId' })`
3. Create a message to sign
```tsx
 const siweInstance = new SiweMessage({
      // this will let the user validate the domain they are logging in to
      domain: window.location.host,
      // this will let the user validate the origin they are logging in to
      uri: window.location.origin,
      address: address,
      statement: 'I am logging in to the SIWE demo',
      version: '1',
      chainId: Number(chainId),
      nonce,
    })
```
4. Sign the message with `window.ethereum.request({
      method: 'personal_sign',
      params: [message, address],
    })`
5. post the signature to the server
```tsx
 const res = await fetch('/api/login', {
      method: 'POST',
      body: JSON.stringify({ message, signature, address }),
    })
    const data = await res.json()
```
### Verify the signature

Then we can move to the server and verify the signature. This will happen inside the `api/login` route which will be called when the user clicks the connect button.

__[See the full API route](https://github.com/MetaMask/examples/tree/main/examples/metamask-siwe/pages/api/login.ts)__

In this API route, we'll focus on the following steps:

1. Verify the signature
2. Ensure the signature is sent from the correct address
3. Store the signature in a session

With this done, you now have full access to the users signature and can use it to authenticate the user on your web3 platform or dApp. The interesting part is that you now also have a session containing the address of the user.

This is useful for prefetching data about the user, for example, you can use the address to fetch data related to the user's address all while keeping the user's privacy intact. 

If done well, digital identity in Web3 can provide a more secure and private way to handle user identities all while providing a great user experience.

## Conclusion

In conclusion, digital identity in Web3 is an important topic that is gaining more and more attention as the decentralized web continues to grow. Implementing digital identity in Web3 can be done using various methods, including DIDs, smart contract-based identity protocols, and Metamask and Next.js. By using these tools and methods, individuals can take control of their own digital identity and use it to authenticate and authorize themselves on web3 platforms and dApps.

In order for digital identity in Web3 to be successful, it's important for individuals, developers, and businesses to continue to educate themselves on the benefits and best practices for implementing digital identity in a secure and decentralized manner. With the right tools and knowledge, digital identity in Web3 can provide a more secure and private way to handle user identities.
