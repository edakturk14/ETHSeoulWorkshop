# ETH Seoul Workshop

1. Go to: https://scaffoldeth.io/
Before you begin, you need to install the following tools:

- [Node](https://nodejs.org/en/download/) (v18 LTS)
- Yarn (v1 or [v2+](https://yarnpkg.com/getting-started/install))
- [Git](https://git-scm.com/downloads)
- [VS Code](https://code.visualstudio.com/) 

2. Use the npx command: 'npx create-eth@latest' to bootstrap the project directly.
Make sure that you install the packages when asked.You can choose between Hardhat or Foundry when prompted. 

3. Start your app
- yarn chain
- yarn start
- yarn deploy

4. Edit your smart contract. 

- For this example I have added transfer ownership. 

    function updateOwner(address _newOwner) public {
        owner = _newOwner;
    }

- Then add the isOwner modifier so that only the owner can update it

  function updateOwner(address _newOwner) public isOwner{
        owner = _newOwner;
    }

5. Deploy your smart contract. 

- yarn deploy    

6. Build the frontend.

In this example I'll get the user address 
- Add the address
  const { address: connectedAddress } = useAccount();
- Add the card 
(go to dasiyui and get a frontend card)
- Add the address compontent 
<Address address={connectedAddress} />

7. More frontend: Get the contract owner address 
- Get the contract owner
  const { data: owner } = useScaffoldContractRead({
    contractName: "YourContract",
    functionName: "owner",
  });
- Display the contract owner 
<Address address={owner} />

8. Frontend: update the owner 
- Add AddressInput field to get a new address from the user:
    New Owner: 
    <AddressInput 
        value={newAddress} 
        onChange={setNewAddress} 
    />
- Add the constants:
const [newAddress, setNewAddress] = React.useState<string>("");
- Create onClick function:
  const { writeAsync: updateOwner } = useScaffoldContractWrite({
    contractName: "YourContract",
    functionName: "updateOwner",
    args: [newAddress],
  });
- Add onClick Function to the button:
    onClick={() => updateOwner()

9. Deploy the contract 
yarn generate 
yarn account 
yarn deploy --network sepolia
yarn verify --network sepolia 







