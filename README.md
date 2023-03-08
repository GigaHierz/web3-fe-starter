# Leipzig DAO FE development workshop

We are using the [ethers.js](https://docs.ethers.org/v5/getting-started/) library to interact with the blockchain.

The easiest way for us will be to just use our Wallet to connect with the blockchain.

ATTENTION: For web3 webdevelopment it is very important that you are not mixing your development wallets/ keys/ accoutns with your actual accounts.
In Google you have the option to create different profiles, so I have one Web3 development profile.

So please make sure you have the [MetaMask](https://metamask.io/) extension for your browser installed: but not the one you have actually coins on. If you only have a real one, get a new one for development.

## 1. Import the [ethers.js](https://docs.ethers.org/v5/getting-started/) library into your browser

Create an `index.html` file and put in this line of code:

```
<script
    charset="utf-8"
    src="https://cdn.ethers.io/scripts/ethers-v4.min.js"
    type="text/javascript"
></script>
```

Your code should look like this now:

```
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script
      charset="utf-8"
      src="https://cdn.ethers.io/scripts/ethers-v4.min.js"
      type="text/javascript"
    ></script>
  </body>
</html>
```

-> Run the doc in Liveserver and let's connect to the Blockchain (in this case Ethereum)

2. Connecting to Ethereum through MetaMask

The quickest and easiest way to experiment and begin developing on Ethereum is to use MetaMask, which is a browser extension that provides:

A connection to the Ethereum network (a Provider)
Holds your private key and can sign things (a Signer)

-> Open your console and input to get our provider which MetaMask already injects as standard into each page

```
const provider = new ethers.providers.Web3Provider(window.ethereum)
```

next we need to request permission to connect to the users wallet account. After you entered this command, your wallet will open and you will have to give permission to the page to connect to your wallet.

```
await provider.send("eth_requestAccounts", []);
```

To sign transactions, to pay something and to write on the blockchain, we need the account signer to sign transactions

```
const signer = provider.getSigner()
```

## 3. Querying the Blockchain

Once you have a Provider, you have a read-only connection to the blockchain, which you can use to query the current state, fetch historic logs, look up deployed code and so on.

Get the current Block number

```
await provider.getBlockNumber()
// 16784122
```

Get the balance of ETH your account currently holds

```
balance = await provider.getBalance("gigahierz.eth")
// { BigNumber: "182334002436162568" }
```

Often you need to format the output to something more user-friendly, such as in ether (instead of wei)

```
ethers.utils.formatEther(balance)
// '0.029441893996447013'
```

## 4. Writing to the Blockchain

First we want to change to a testnet. Because of course we don't want to send real ETH.

So please in your wallet choose to show Testnets and then choose "Sepolia" Network.

```
const tx = signer.sendTransaction({
    to: "0x78344979959C9d25Beb73748269A2B5533F87a51",
    value: ethers.utils.parseEther("0.001")
});
```
