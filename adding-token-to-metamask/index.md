## Introduction

We often discuss topics the user experience of Dapps and how to connect them MetaMask. At MetaMask, is stride to empower Dapp developers to build the best possible user experience for their users. We want to make it as easy as possible for users to connect to Dapps, and we want to make it as easy as possible for Dapp developers to integrate MetaMask into their Dapps.

An element central in many decentralized project is their own token. Such tokens drive a lot of communities simply because they are the native currency of the project. In this tutorial, we will how you can programmatically prompt a user to add a token to MetaMask.

## What do we need before?

There are a few requirements for adding a token to MetaMask programmatically:

1. The user must have MetaMask installed
1. The user must have accepted the connection request from the Dapp
1. You must have a contract address for the token you want to add

Today however we won't focus on these requirements. If you want to learn these different actions, here are a few resources.

1. How to detect if MetaMask is installed: [MetaMask Docs](https://docs.metamask.io/guide/getting-started.html#web3-browser-detection)
1. How to request a connection: [MetaMask Docs](https://docs.metamask.io/guide/getting-started.html#connecting-to-metamask)
1. Making a Token Contract: [Ethereum.org](https://docs.openzeppelin.com/contracts/4.x/erc20)

Now that we have the requirements out of the way, let's get started!

## Adding a token to MetaMask

Adding a token to a wallet is defined in [EIP-747](https://eips.ethereum.org/EIPS/eip-747). This is implemented in MetaMask as the `wallet_watchAsset` RPC method. This RPC method is exposed by the `ethereum` object injected by MetaMask. This RPC method takes a single object parameter with the following properties:

```tsx
ethereum.request({
  method: "wallet_watchAsset",
  params: {
    type: "ERC20", // For now, only ERC20 is supported but support for NFT tokens is being worked on
    options: {
      address: "0xb60e8dd61c5d32be8058bb8eb970870f07233155", // The address of the smart contract supporting the token
      symbol: "FOO", // A ticker symbol or shorthand
      decimals: 18, // The number of decimals in the token
      image: "https://foo.io/token-image.svg", // A string url of the token logo
    },
  },
});
```

Passig this method call to a button click handler is all you need to add a token to MetaMask. Let's see how we can do this in a React app.

```tsx
import React from "react";

export const Button = () => {
  const [loading, setLoading] = React.useState(false);

  const addToken = async () => {
    setLoading(true);
    try {
      const res = await ethereum.request({
        method: "wallet_watchAsset",
        params: {
          type: "ERC20",
          options: {
            address: "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
            symbol: "FOO",
            decimals: 18,
            image: "https://foo.io/token-image.svg",
          },
        },
      });

      if (res) {
        console.log("Token was added!");
      } else {
        throw new Error("User refused to add token");
      }
    } catch (error) {
      // In the case a user rejects the request, you will be prompted with an error and can handle it here E.G. show a message to the user
      console.log(error);
    } finally {
      setLoading(false);
    }
  };

  return <button onClick={addToken}>Add Token</button>;
};
```

As you can see, adding a token to MetaMask is as simple as calling the `wallet_watchAsset` RPC method. This method returns a promise that resolves to a boolean. If the user accepts the request, the promise will resolve to `true`. If the user rejects the request, the promise will resolve to `false`.

## Conclusion

In this tutorial, we went over the basics of adding a token to MetaMask programmatically. We saw how to add a token to MetaMask by calling the `wallet_watchAsset` RPC method. We also saw how to handle the user's response to the request.

We encourage you to try this out in your own Dapp. If you have any questions, feel free to reach out to us on [Twitter](https://twitter.com/MetaMaskDev).
