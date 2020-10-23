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

Great, you've entered the values. Hit the "connect to web3" prompt and once you're connected send off the tx!

### Step 2

Once the transaction has been mined, you will need to go into the logs to discover where the vesting contract was deployed to. While in _the transaction view_, click on the `Logs` tab at the top. You should see two events. Look for the one named `TokenVestingDeployed`, and find the first argument. It should be called `location`. That is the address of the vesting contract. You can click on it to be brought there.

I _believe_ that once you arrive, the contract will already be verified, and as such, you should be able to click on the "contract" tab, and find the "Read Contract" and "Write Contract" buttons. This is the interface you can use to verify that everything went as expected, and it's also the page you can send to the recipient that they can use to cause withdrawals.

To sanity check the values that are shown under "Read Contract", you can check that `duration` is exactly what you expected, and that `cliff` is equal to `start` plus however long you wanted to wait for vesting to begin. So if you wanted vesting to begin immediately, then `start = cliff`. Finally, check that the beneficiary is who you expected (the recipient, same thing).

### Step 3

Send the RSR to the deployed TokenVesting contract! This is the contract you were working on above where you could read out the `cliff`, `duration`, and `start` values. That's it! The beneficiary can call `release` function whenever they want to have all the tokens available to them at that time to be disbursed.
