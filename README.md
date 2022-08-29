# Karani

## Introduction

Karani is blockchain based land registry written in NodeJS.

## System Overview
![blockchain](https://user-images.githubusercontent.com/18010106/187301975-b4046b6f-9796-41a4-b668-a8aef5bddf4a.png)

Let's say Bob wants to buy Land from Alice.

1. First Bob has to confirm with the system if Alice is indeed the owner and not a scammer, we will come back to how Bob does this. Let's assume that Bob has indeed undoubtedly confirmed that Alice is the rightful owner of the piece of land.
2. Once Bob and Alice agree on the price, Alice has to sign a transfer document using her private key, indicating that she has indeed transfered land to Bob, through a Digital Signature appended to the document.
3. She then uploads this transfer document to Karani.
4. The Land Office (government server) does some very basic checks on the uploaded document (Person is logged in and has uploaded a non-corrupt file)
5. The Land Office then creates what is called a block proposal where the main transaction is a land transfer. It sends this proposal to the "blockchain" for other nodes to verify
6. The other nodes then proceed with verification. For land transfer. They first check if the Digital Signature is valid. They do this by using Alice's public key that they have on file.
7. Note that each node has a separate and independent database, ensuring that if someone changed Alice public key in one node,  the other nodes have the correct one. (70% of nodes have to have consensus for the block proposal to get approved)
8. Once they confirm. Each node signs that they have confirmed the block proposal and forwards the request to an aggregator, whose sole job is to append all the signatures of the nodes to the block proposal and send the result back to the nodes.
9. Each node then verifies that all the signatures are valid. If there are valid responses from at least 70% of the nodes the block gets added to the blockchain, and all database/state changes are made/committed.
10. And now Bob is the rightful owner of the Land.

## Repositories
The application is divide into the following repositiories
1. Sahihi - digital signature tool for browsing the blockchain and verify digital signatures.
2. Karani Frontend - acts as a portal between users and the blockchain
3. Karani Backend - used for basic authentication, validation and block proposals. This is the backed to Karani Frontend 
4. Karani Peer - this the block chain node for Karani. The primary purpose of this server is validation of transactions, which are contained in block proposals. Transactions may include:
5. Karani Aggregator - is responsible for aggregating signtures from the nodes , and sending the result back to the nodes. The nodes then decided indendently to add the block to the blockchain based on the percent of valid signatures. The block is committed when atleast 70% valid node/peer signatures are contained in the block proposal.
