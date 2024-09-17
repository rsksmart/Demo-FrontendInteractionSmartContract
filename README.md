
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


## Disclaimer
The software provided in this GitHub repository is offered “as is,” without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement.
- **Testing:** The software has not undergone testing of any kind, and its functionality, accuracy, reliability, and suitability for any purpose are not guaranteed.
- **Use at Your Own Risk:** The user assumes all risks associated with the use of this software. The author(s) of this software shall not be held liable for any damages, including but not limited to direct, indirect, incidental, special, consequential, or punitive damages arising out of the use of or inability to use this software, even if advised of the possibility of such damages.
- **No Liability:** The author(s) of this software are not liable for any loss or damage, including without limitation, any loss of profits, business interruption, loss of information or data, or other pecuniary loss arising out of the use of or inability to use this software.
- **Sole Responsibility:** The user acknowledges that they are solely responsible for the outcome of the use of this software, including any decisions made or actions taken based on the software’s output or functionality.
- **No Endorsement:** Mention of any specific product, service, or organization does not constitute or imply endorsement by the author(s) of this software.
- **Modification and Distribution:** This software may be modified and distributed under the terms of the license provided with the software. By modifying or distributing this software, you agree to be bound by the terms of the license.
- **Assumption of Risk:** By using this software, the user acknowledges and agrees that they have read, understood, and accepted the terms of this disclaimer and assumes all risks associated with the use of this software.