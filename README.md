
# DApp Interaction with Smart Contract - RainbowKit & Next.js

This project demonstrates the integration of a decentralized application (DApp) frontend with a smart contract deployed on the Rootstock (RSK) testnet. The frontend is built using Next.js and utilizes **RainbowKit** for wallet management, allowing seamless interaction between the user and the smart contract.

## Features

- **Wallet Connection**: Users can easily connect their wallet (e.g., MetaMask) to interact with the DApp.
- **Read and Write Operations**: The DApp allows users to store a value in the smart contract and retrieve the stored value.
- **RSK Testnet**: The DApp connects to the Rootstock testnet for testing purposes.

## Prerequisites

Before starting, ensure you have the following installed:

- **Node.js** (v14.x or later)
- **npm** (v6.x or later)
- A test wallet account in **MetaMask** or any supported wallet provider.

## How to Run the Project

### 1. Clone the Repository

```bash
git clone https://github.com/rsksmart/Demo-FrontendInteractionSmartContract.git
cd Demo-FrontendInteractionSmartContract
```

### 2. Install Dependencies

Run the following command to install all required dependencies:

```bash
npm install
```

### 3. Run the Development Server

After the installation is complete, run the following command to start the development server:

```bash
npm run dev
```

This will launch the application on `http://localhost:3000/`. Open your browser and go to this URL.

### 4. Configure the Smart Contract Interaction

Navigate to `src/pages/index.tsx` and ensure that the contract address and ABI are set up correctly.

```ts
// Contract ABI
const contractABI = [
  {
    inputs: [
      {
        internalType: 'uint256',
        name: 'value',
        type: 'uint256',
      },
    ],
    name: 'store',
    outputs: [],
    stateMutability: 'nonpayable',
    type: 'function',
  },
  {
    inputs: [],
    name: 'retrieve',
    outputs: [
      {
        internalType: 'uint256',
        name: '',
        type: 'uint256',
      },
    ],
    stateMutability: 'view',
    type: 'function',
  },
];

// Contract Address (change it to your deployed contract address)
const contractAddress = '0xYourContractAddressHere';
```

Make sure to replace `'0xYourContractAddressHere'` with the actual address of the deployed contract.

### 5. Connect Wallet

Once the application is running, follow these steps to connect your wallet:

1. Open the application in the browser.
2. Click on the **Connect Wallet** button.
3. Select **MetaMask** or any other supported wallet.
4. Ensure you are connected to the **RSK Testnet** network.

### 6. Interact with the Smart Contract

Once connected, you can:

- **Store a Value**: Enter a number in the input field and click the **Store Value** button. This will call the `store` function of the smart contract and store the entered value.
- **Retrieve the Stored Value**: Click the **Retrieve Stored Value** button to call the `retrieve` function and display the stored value.

### 7. Testing on RSK Testnet

Always use test wallets when interacting with contracts on testnets. Never use real funds during development to avoid the risk of losing your assets.

## Code Overview

### `src/pages/index.tsx`

This is the main file where the frontend logic resides. It includes two main functions:

- `useReadContract`: Reads the value from the smart contract using the `retrieve` function.
- `useWriteContract`: Writes a new value to the smart contract using the `store` function.

### Example Code Snippets

#### Read from Smart Contract

```ts
const {
  data: retrievedValue,
  error: errorRetrieve,
  isPending: isPendingRetrieve,
} = useReadContract({
  address: contractAddress,
  abi: contractABI,
  functionName: 'retrieve',
  args: [],
  chainId: 31, // RSK Testnet chain ID
});
```

#### Write to Smart Contract

```ts
const { data: hash, writeContract, isSuccess, isPending, isError } = useWriteContract();

const handleWriteContract = async () => {
  console.log('Recording new value:', inputValue);
  writeContract({
    address: contractAddress,
    abi: contractABI,
    functionName: 'store',
    args: [inputValue],
  });
};
```

## Important Notes

- **Testnet Environment**: The DApp runs on the Rootstock (RSK) testnet, so ensure your wallet is set to the correct network.
- **Testing with Test Wallets**: Always use test wallets with no real assets during development to avoid the risk of losing funds.
- **Contract Deployment**: The smart contract should already be deployed on the RSK testnet. If not, deploy the contract and update the address in the frontend accordingly.

## Resources

- [RainbowKit Documentation](https://www.rainbowkit.com/docs)
- [RSK Testnet Information](https://developers.rsk.co/rsk/running-testnet/)
- [Wagmi Documentation](https://wagmi.sh/docs)
