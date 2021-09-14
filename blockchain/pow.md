# Proof of work


## Concept 

The concept of pow is to create a kind of job that is hard to solve but easy to verify. In the context of bitcoin and most of the crypto currency, this means to "mine" a hash function that is below the a certain threshold value. Therefore, the diffculty could be controled by the leading zero of the target hash result, the smaller the threshold the harder the hash.

In order to let the current block of transactions to fulfill the target, the miner needs to add value to the "nounce" field of the block, which randomly change the resulting hash value to a different number. The entire process does not have any solution or algorithm that can boost the brote-force operations, and the result is just pure luck.

## Example

Reference link: https://en.bitcoin.it/wiki/Proof_of_work