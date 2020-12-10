# Vesting

Simple easy-to-use factory etherscan interface for locking up tokens.

## How to use

### Step 1

Go here: https://etherscan.io/address/0xdf337057167ec910c6d7f75c123ac8e22f11da47#writeContract

You'll see three parameters you will need to come up with. They're pretty straightforward though.

1. `recipient`: the recipient's address
2. `startVestingInThisManySeconds`: This is verbose on purpose!. If you want the vesting to begin now, set this to 0.
3. `vestForThisManySeconds`: how long the vesting should last, in seconds, once it has begun.

The only tricky part is calculating things in terms seconds. Here's an example of how you would calculate two years.

```
    60*60*24*365*2=63,072,000.
```

Great, you've entered the values. Hit the "connect to web3" prompt. Once you're connected, send off the tx! You'll probably want to use the "fast" gas setting.

### Step 2

After the tx has been sent, a new button labeled "view your transaction" should appear. Click on that. Wait for mining.

Once the transaction has been mined, click on the "Logs" tab at the top. You should see two events. Look for the one named `TokenVestingDeployed`, and find the first argument. It should be called `location`. That is the address of the vesting contract. You can click on it to be brought there. You'll know you're in the right place if you end up on a contract page, and it has no past txs.

### Step 3

Great! You've found the address of your newly deployed vesting contract!
Send the RSR you would like vested to this address, in a normal RSR transfer.

### Step 4 (For the beneficiary)

The beneficiary will need to interact with your newly deployed vesting contract in order to retrieve their RSR at the end of the vesting period. Copy the etherscan URL and send it to them, along with the following instructions:

```
When the vesting period is over, you may withdraw your RSR by interacting with this contract on etherscan: <INSERT ETHERSCAN URL>. You'll need a metamask account, or another web3 wallet, to interact with the blockchain. You can check how many tokens are available for withdrawal at any time by clicking on "Contract" -> "Read Contract", and using the `releasable` function, providing the RSR token address (0x8762db106b2c2a0bccb3a80d1ed41273552616e8) as an argument. If you would like to perform the actual withdrawal, go to "Contract" -> "Write Contract", and call the `release` function, also passing in the RSR contract address.
```
