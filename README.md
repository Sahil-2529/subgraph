# subgraph
Real-time Uniswap V3 liquidity monitoring using The Graph for tracking mints and burns.

Title:
Real-Time Liquidity Pool Monitoring on Uniswap V3 Using The Graph

Description:
This query helps track real-time liquidity additions and removals from Uniswap V3 pools, providing crucial data for liquidity providers and traders to understand liquidity dynamics and make informed decisions.

Subgraph to Query:
Uniswap V3 Subgraph

Example Query:
{
  mints(first: 10, orderBy: timestamp, orderDirection: desc) {
    id
    pool {
      token0 {
        symbol
        name
      }
      token1 {
        symbol
        name
      }
      feeTier
    }
    owner
    amount
    amount0
    amount1
    tickLower
    tickUpper
    timestamp
  }
  burns(first: 10, orderBy: timestamp, orderDirection: desc) {
    id
    pool {
      token0 {
        symbol
        name
      }
      token1 {
        symbol
        name
      }
      feeTier
    }
    owner
    amount
    amount0
    amount1
    tickLower
    tickUpper
    timestamp
  }
}

Result of Example Query:

{
  "data": {
    "mints": [
      {
        "id": "0x12345...",
        "pool": {
          "token0": {
            "symbol": "USDC",
            "name": "USD Coin"
          },
          "token1": {
            "symbol": "ETH",
            "name": "Ether"
          },
          "feeTier": "3000"
        },
        "owner": "0xabcde...",
        "amount": "1000",
        "amount0": "500",
        "amount1": "0.25",
        "tickLower": "200000",
        "tickUpper": "210000",
        "timestamp": "1622500000"
      }
      ...
    ],
    "burns": [
      {
        "id": "0x67890...",
        "pool": {
          "token0": {
            "symbol": "DAI",
            "name": "Dai Stablecoin"
          },
          "token1": {
            "symbol": "ETH",
            "name": "Ether"
          },
          "feeTier": "500"
        },
        "owner": "0xfghij...",
        "amount": "500",
        "amount0": "250",
        "amount1": "0.125",
        "tickLower": "190000",
        "tickUpper": "200000",
        "timestamp": "1622600000"
      }
      ...
    ]
  }
}



Title:
Real-Time Liquidity Pool Monitoring on Uniswap V3 Using The Graph

Description:
This query helps track real-time liquidity additions and removals from Uniswap V3 pools, providing crucial data for liquidity providers and traders to understand liquidity dynamics and make informed decisions.

Subgraph to Query:
Uniswap V3 Subgraph

Example Query:
graphql
Copy code
{
  mints(first: 10, orderBy: timestamp, orderDirection: desc) {
    id
    pool {
      token0 {
        symbol
        name
      }
      token1 {
        symbol
        name
      }
      feeTier
    }
    owner
    amount
    amount0
    amount1
    tickLower
    tickUpper
    timestamp
  }
  burns(first: 10, orderBy: timestamp, orderDirection: desc) {
    id
    pool {
      token0 {
        symbol
        name
      }
      token1 {
        symbol
        name
      }
      feeTier
    }
    owner
    amount
    amount0
    amount1
    tickLower
    tickUpper
    timestamp
  }
}
Result of Example Query:
json
Copy code
{
  "data": {
    "mints": [
      {
        "id": "0x12345...",
        "pool": {
          "token0": {
            "symbol": "USDC",
            "name": "USD Coin"
          },
          "token1": {
            "symbol": "ETH",
            "name": "Ether"
          },
          "feeTier": "3000"
        },
        "owner": "0xabcde...",
        "amount": "1000",
        "amount0": "500",
        "amount1": "0.25",
        "tickLower": "200000",
        "tickUpper": "210000",
        "timestamp": "1622500000"
      }
      ...
    ],
    "burns": [
      {
        "id": "0x67890...",
        "pool": {
          "token0": {
            "symbol": "DAI",
            "name": "Dai Stablecoin"
          },
          "token1": {
            "symbol": "ETH",
            "name": "Ether"
          },
          "feeTier": "500"
        },
        "owner": "0xfghij...",
        "amount": "500",
        "amount0": "250",
        "amount1": "0.125",
        "tickLower": "190000",
        "tickUpper": "200000",
        "timestamp": "1622600000"
      }
      ...
    ]
  }
}
Additional Notes:
This query allows users to monitor recent liquidity events (mints and burns) on Uniswap V3 pools, making it invaluable for liquidity providers who need to track their positions and the overall liquidity trends in real-time. Users can adjust the first parameter to retrieve more or fewer records or apply filters for specific token pairs or time ranges.

GitHub Repository:
Uniswap V3 Liquidity Monitoring Example

Social Media Post:
Posted on Twitter:
"Excited to share my latest project! 🚀 Track real-time liquidity pool events on Uniswap V3 using The Graph. Perfect for LPs and traders to stay informed about liquidity dynamics! 📈 #DeFi #Uniswap #TheGraph #Ethereum"

[Thu, 13 Jun 2024 16:10:26 -0800] Program executed in: 2.189s.
✅ Step 2: Create and ship our Subgraph ✅
Now we can open up a fourth window to finish setting up The Graph. 😅 In this fourth window, we will create our local subgraph!

Note: You will only need to do this once.

yarn local-create
You should see some output stating your Subgraph has been created along with a log output on your graph-node inside Docker.

Next, we will ship our subgraph! You will need to give your subgraph a version after executing this command. (e.g., 0.0.1).

yarn local-ship
This command does the following all in one… 🚀🚀🚀

Copies the contracts ABI from the hardhat/deployments folder
Generates the networks.json file
Generates AssemblyScript types from the subgraph schema and the contract ABIs.
Compiles and checks the mapping functions.
… and deploys a local subgraph!
If you get an error ts-node, you can install it with the following command

npm install -g ts-node
You should get a build completed output along with the address of your Subgraph endpoint.

Build completed: QmXyZWsVSUYTd1dJnqn84kJkDggc2GD9RZWK5xLVEMB9iP

Deployed to http://localhost:8000/subgraphs/name/scaffold-eth/your-contract/graphql

Subgraph endpoints:
Queries (HTTP): http://localhost:8000/subgraphs/name/scaffold-eth/your-contract

✅ Step 3: Test your Subgraph ✅
Go ahead and head over to your subgraph endpoint and take a look!

Here is an example query…

  {
    mints(first: 10, orderBy: timestamp, orderDirection: desc) {
      id
      pool {
        token0 {
          symbol
          name
        }
        token1 {
          symbol
          name
        }
        feeTier
      }
      owner
      amount
      amount0
      amount1
      tickLower
      tickUpper
      timestamp
    }
    burns(first: 10, orderBy: timestamp, orderDirection: desc) {
      id
      pool {
        token0 {
          symbol
          name
        }
        token1 {
          symbol
          name
        }
        feeTier
      }
      owner
      amount
      amount0
      amount1
      tickLower
      tickUpper
      timestamp
    }
  }
If all is well and you’ve sent a transaction to your smart contract, then you will see similar data output!

Next up, we will dive into a bit more detail on how The Graph works so that as you start adding events to your smart contract, you can start indexing and parsing the data you need for your front-end application.

A list of all available commands
run-node
yarn run-node
Spin up a local graph node (requires Docker).

stop-node
yarn stop-node
Stop the local graph node.

clean-node
yarn clean-node
Remove the data from the local graph node.

local-create
yarn local-create
Create your local subgraph (only required once).

local-remove
yarn local-remove
Delete a local subgraph.

abi-copy
yarn abi-copy
Copy the contracts ABI from the hardhat/deployments folder. Generates the networks.json file too.

codegen
yarn codegen
Generates AssemblyScript types from the subgraph schema and the contract ABIs.

build
yarn build
Compile and check the mapping functions.

local-deploy
yarn local-deploy
Deploy a local subgraph.

local-ship
yarn local-ship
Run all the required commands to deploy a local subgraph (abi-copy, codegen, build, and local-deploy).

deploy
yarn deploy
Deploy a subgraph to TheGraph.
