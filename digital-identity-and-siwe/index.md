# Introduction

Everywhere you go, you have a digital identity. This identity is the collection of data that represents your activity online. It is challenging to stay truly anonymous online in this era of social media.

If you are present on a social like Facebook or TikTok, you probably have seen disturbing advertisements after visiting a website seemingly unrelated to those platforms. This is because websites implement a variety of cross-site tracking technologies, identifying you across the Internet.

## An Overview of Digital Identity In Present-Day Earth, 2023

"Digital Identity" refers to a person or entity's identity existing in the digital world. It encompasses the information, attributes, and characteristics associated with a person or entity. You can use identity for various purposes, such as authentication, authorization, and access control. In tech jargon, a digital identity is an online or networked identity adopted or claimed in cyberspace by an individual, organization, or electronic device.

Digital identities can be centralized or decentralized, depending on how they are created and managed. Centralized digital identities are controlled by a single entity, such as a government or a corporation, while decentralized digital identities are controlled by the individual or entity they represent.

A user's digital identity can have simple attributes like:

- Name
- Address
- Username and password
- Date of birth

Or complex attributes such as:

- Online search activities, like electronic transactions
- Social security number
- Medical history
- Purchasing history or behavior
- Biometric data
- Digital certificates

In multiple industries, we see use cases for digital identities, such as finance, healthcare, and e-commerce, and uses, such as online banking, secure messaging, and personal data management.   

A widespread issue plaguing digital identity on the Internet is Identity theft, so the subject of digital identity authentication and validation measures are critical to ensuring Web and network infrastructure security in the public and private sectors. Admittedly, there has been a lot of talk about authentication. With the advent of blockchain technology, we are seeing the use of digital identities in decentralized applications and platforms built on the blockchain. Recently, the Web3 community has become fragmented around multiple wallets and authentication methods. 

Web3 developers are digital self-sovereignty advocates so let’s look at what the concept of digital identity means in web3.

## Identity in Web3 and Its Implementation

Identity in web3 refers to self-sovereign identity, allowing individuals to own and control their digital identity. Centralized entities such as governments and corporations control Identities in traditional web2 systems. In web3, individuals can create and manage their digital identities using blockchain technology.

There are several methods of implementing identity in web3, with popular ones such as Decentralized Identity Protocols(DID) and Smart Contract-based Identity Protocols, and others like Self-sovereign identity (SSI) systems, Public Key Infrastructure (PKI) based systems and Biometric-based Identity as well.

1. Decentralized Identity (DID): These protocols allow users to create and manage their own digital identities on the blockchain. DIDs are unique identifiers registered on a blockchain and can be used to authenticate and authorize individuals on the web3 network. Then be used to link different identities, such as social media and email, to a single blockchain-based identity.

2. Smart Contract-based Identity: These protocols use smart contracts to store and manage user identities on the blockchain. Users can create and manage their identities using smart contracts, which can also be used to authenticate and authorize users on web3 applications.

3. Self-sovereign identity (SSI): Systems based on the same principles of DIDs; however, they allow the user to hold and control their identity data without needing a centralized entity.

4. Public Key Infrastructure (PKI): PKI-based systems use digital certificates and public and private keys to authenticate and authorize users on web3 applications. Similar to traditional web2 systems.

5. Biometric-based Identity: Biometrics such as fingerprints, facial recognition, and voice recognition can be used to create and authenticate digital identities on web3.

With web3, individuals have more control over their data and identity, allowing them to share it selectively and revoke access anytime. Additionally, it also allows to have multiple identities, and connect them in a way that they can be used to prove the identity of the user. It is pertinent to remember, that the implementation of some of these methods are still in the early stages and there are still ongoing research and development to make them more user-friendly and widely adopted.

Blockchain developers have long talked about developing "decentralized" identity standards to save users from the dangers of Big Login, and this birthed: Sign-in With Ethereum proposal, a digital identity standard which was built by the community with direct support from the Ethereum Foundation and ENS, with Spruce Systems tapped to lead the charge.

## How the Sign In With Ethereum Proposal Affects Digital Identity

The Sign In With Ethereum(SIWE) proposal was a proposed standard for using Ethereum to authenticate and authorize users on web3 applications. It aimed to provide a standard way for users to sign in to web3 applications using their Ethereum address and private key, similar to how users currently sign in to web2 applications using their email and password. It uses a private key to authenticate a user's identity on the Ethereum blockchain. A private key is a unique string of characters associated with an Ethereum address and is used to sign digital transactions. When a user signs in with Ethereum, they provide a digital signature using their private key to prove that they are the owner of the Ethereum address. This proposal allows them to access their account and perform actions such as sending and receiving Ether, interacting with smart contracts, and more.

With SIWE, users would create an Ethereum address and private key specifically for signing in to web3 applications. When they want to sign in to a web3 application, they will use their private key to sign a message proving they are the owner of the Ethereum address. The web3 application would then verify the signature and authenticate the user.

SIWE affects digital identity by:

- Allowing individuals to use their Ethereum address as a way to authenticate on web3 applications.
- Eliminating the need for complexe passwords and usernames.
- Allowing users to use their Ethereum address as a decentralized identity across different web3 applications.
- Enabling web3 applications to authenticate and authorize users without the need for centralized identity providers, such as social media login or email and password, which could lead to more privacy and security for the user.

The idea behind the proposal is to standardize the way you authenticate with a digital identity. The following steps are followed:

- A server creates a unique number called a Nonce for each user that will sign-in.
- A user requests to connect a site with their wallet.
- The user is presented with a unique message that indicates the Nonce and information about the website.
- The user signs in with their wallet.
- The user is then authenticated and the website is given access to data about the user that was approved.

MetaMask is a popular tool and a browser extension that allows users to interact with the Ethereum blockchain and can be used to implement digital identity and SIWE. MetaMask can be used to create and manage Ethereum addresses, which can be used as a digital identity on web3 platforms and dApps.

For your users, the experience is simple, but multiple steps are happening behind the scenes.

## How to Implement Sign-In With Ethereum

As mentioned above, we will need to generate a unique number called a Nonce; since this should be done on a server, we will be working with Next.js, the most popular React framework for building server-side rendered applications.

We will be starting from a basic Next.js application created with [`create-next-app`](create-next-app), and we will use the following
libraries:

- [`@metamask/providers`](https://www.npmjs.com/package/@metamask/providers) - A library for interacting containing TypeScript types for the MetaMask provider API.
- [`ethers`](https://www.npmjs.com/package/ethers) - A library containing different utilities for interacting with the Ethereum blockchain.
- [`siwe`](https://www.npmjs.com/package/siwe) - A library containing utilities for implementing Sign In With Ethereum.
- [`iron-session`](https://www.npmjs.com/package/iron-session) - A library for implementing session management in Next.js applications.

**N.B. The complete code is [available here](https://github.com/MetaMask/examples/tree/main/examples/metamask-siwe).**

### A Dance Between the Client and the Server

With these libraries, we can lay down the architecture for implementing SIWE. To connect users, we will want to implement the following:

1. Generate a Nonce inside `getServerSideProps`
2. Pass the Nonce to the client
3. Connect to a user's wallet
4. Make the user sign a message containing the Nonce
5. Verify the signature
6. Store the signature in a session

###  Generate a Nonce inside `getServerSideProps`

Our first step is to generate a Nonce inside `getServerSideProps` of our login page, which is located at `pages/login.tsx`.

Generating the Nonce inside `getServerSideProps` is crucial because execution happens on the server, and we can pass it to the client. This is faster than fetching it from an API route like in other implementations.

```tsx
export const getServerSideProps = () => {
  const nonce = generateNonce();

  return {
    props: {
      nonce,
    },
  };
};
```

With this, we can now pass the nonce to the client.

###  Passing Our Nonce to the Client

Next, we will pass the Nonce to the client. This will happen by defining a default export for the login page, which will be a React component that will receive the Nonce as a prop.

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

With this done, you now have full access to the user's signature and can use it to authenticate the user on your web3 platform or dApp. The interesting part is that you now also have a session containing the user's address.

This is useful for prefetching data about the user; for example, you can use the address to fetch data related to the user's address, all while keeping the user's privacy intact. 

If done well, digital identity in Web3 can provide a more secure and private way to handle user identities, all while providing a great user experience.

## Conclusion

In conclusion, digital identity in Web3 is a critical topic that is gaining more and more attention as the decentralized Web continues to grow. Implementing digital identity in Web3 can be done using various methods, including DIDs, smart contract-based identity protocols, and Metamask and Next.js. By using these tools and techniques, individuals can take control of their digital identity and use it to authenticate and authorize themselves on web3 platforms and dApps.

In order for digital identity in Web3 to be successful, individuals, developers, and businesses need to continue to educate themselves on the benefits and best practices for implementing digital identity in a secure and decentralized manner. With the right tools and knowledge, digital identity in Web3 can provide a more secure and private way to handle user identities.
