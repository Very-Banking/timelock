![50x50](https://user-images.githubusercontent.com/118863576/205505593-18a8a22d-20ee-45f2-bed6-b6c86f5c2ed5.png)
# Timelock
A simple timelock smart contract which will be used for vesting <b>$VB</b> tokens against a certain period of time then allows a set of users to withdraw the tokens when the time period has elapsed. We propose several usecases below.<p>
* Early adopter vested bonus bag as per PEGP-001
* Locking up based on proposed token economics as per whitepaper
## Instructions
### 1. Import
Import the contract into desired editor
### 2. Compile
Compile `timelock.sol` in your desired editor
### 3. Deploy
Deploy the `timelock.sol` contract; making sure that “Contract” section is set to `VBTimelock`

Ensure you use the <b>$VB</b> token contract address when deploying.
### 4. Set Timestamp
Set the timestamp of the contract by calling the `setTimestamp` function. There is only one function parameter called `_timePeriodInSeconds`; which reflects the amount of time (in seconds) for which you want the time lock period to exist.

If you call the `timestampSet` function you will recieve a `boolean` value whether the timestamp is set. A `true` response means the `setTimestamp` function has been set and is active.

If you call the `initialTimestamp` fuction you will be able to confirm the value in proper date format using an epoch to date converter
### 5. Set Contract Address
Check to make sure the ERC20 contract associated with this timelock contract is correct (in our case <b>$VB</b>). You may call the `erc20Contract` variable, to see which contract is currently set (this is the address you selected upon deployment).
### 6. Allocate
Allocating user tokens into the timelock contract. Tokens can be allocated to users one at a time using the `depositToken` function or `bulkDepositTokens`. Always keep an exact record of how many tokens (sum total of all <b>$VB</b> tokens) which has been allocated to the users. This sum total figure is required for the next step (and ensures that there will be the exact amount of tokens in the timelock contract to service all of the users, who will be performing the unlock).
### 7. Transfer
From the ERC20 token contract, use the `transfer` function to transfer <b>$VB</b> tokens to the timelock smart contract's address.
### 8. Finalize
Once all allocations have been made and the <b>$VB</b> tokens have been transferred into the timelock contract, the owner can call the timelock contract's `finalizeAllIncomingDeposits` function. This makes the contract completely non-custodial, whereby the contract owner has no ability to alter token amounts gooing forward and so forth. The operation of the timelock contract is purely based on the math in the `transferTimeLockedTokensAfterTimePeriod` function from this point forward.

## Thanks
https://github.com/second-state

https://github.com/tpmccallum
