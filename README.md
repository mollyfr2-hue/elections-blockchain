# elections-blockchain
Final project in Blockchain Course
A default elections project built according to the course requirements: an admin interface, candidate management, a voter registry using a Merkle tree, a voting time window, winner and ranked results display, an ERC20 reward token named BAL, and a bonus feature: an “anonymous” choice via a client-side questionnaire (3 topics).

Requirements

Node.js 18+

MetaMask

Recommended network: Sepolia

Installation & Local Run
1) Smart Contracts (Hardhat)
cd hardhat
npm install
cp .env.example .env
# Fill in PRIVATE_KEY and SEPOLIA_RPC_URL
npx hardhat compile
npx hardhat test
npx hardhat run scripts/deploy.js --network sepolia

At the end, contract addresses are printed to the console and saved to hardhat/deployments/sepolia.json.

2) Voter Registry (Merkle)

Create a voter addresses file at hardhat/allowlist.json (an array of addresses). Then run:

cd hardhat
node scripts/buildMerkle.js

The script prints the Merkle Root and generates hardhat/merkle.json containing proofs for each address.

3) Frontend
cd frontend
npm install
cp .env.example .env
# Update VITE_ELECTION_ADDRESS and VITE_CHAIN_ID
npm run dev
End-to-End Flow

The admin deploys the contracts and sets the Merkle Root, voting time window, and reward.

A voter connects with MetaMask, verifies eligibility via a Merkle proof, and votes within the allowed time window.

After the voting window closes, ranked results are displayed.

The voter claims and automatically receives BAL tokens once voting has ended.

Known Bugs / Transparent Notes 

the choice is computed client-side, and the voter is not shown which candidate was selected. However, anyone inspecting the transaction data can infer the candidateId (public blockchain). This provides UX-level anonymity only.

Results sorting is done on-chain using a simple algorithm (intended for a small number of candidates).

Note:
These instructions explain how to run the project using the Windows Command Prompt (CMD).
You will need three separate CMD windows. Please follow the steps in order.

Step 1: Start the Local Hardhat Network

Open a CMD window.

Navigate to the Hardhat directory:

cd elections-dapp/hardhat

Install dependencies:

npm install

Start the local Hardhat node:

npx hardhat node

Note:
At this point, you should see output similar to:

Account #0: 0xf39Fd6...

This means the local blockchain is running.

Step 2: Deploy the Smart Contracts

Open a second CMD window.

Navigate again to the Hardhat directory:

cd elections-dapp/hardhat

Deploy the contracts to the local network:

npx hardhat run scripts\deploy.js --network localhost

Note:
You should see output similar to:

Contract deployed to: 0x...

This confirms the contracts were deployed successfully.

Step 3: Run the Frontend

Open a third CMD window.

Navigate to the frontend directory:

cd elections-dapp/frontend

Install frontend dependencies:

npm install

Start the frontend:

npm start

If that does not work, run:

npm run dev
