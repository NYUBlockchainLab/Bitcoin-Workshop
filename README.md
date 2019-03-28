Outline
Introduction
Traditionally, commerce on the Internet has relied exclusively on financial institutions serving as a trusted third party to process electronic payments 
Ex: Purchasing something on eBay, put in credit card information, your credit card company relays with your bank to subtract some balance from your account, then relays to the merchant’s bank to add that balance to their account
What exactly is happening here?


For the most part, even today, this is completely acceptable and works perfectly fine
But there is still many weaknesses of relying on a trusted third party, namely:
Requiring full KYC for accountability purposes
Many fees along the pipeline (more parties involved, more want a ‘piece of the cake’)
What Satoshi has proposed is this system or protocol, that if you join and play by the rules, two parties can transact directly to one another without the need for a trusted third party. 
a “purely P2P version of electronic cash that would allow online payments to be sent directly from one party to another without going through a financial institution”
Transactions
The first thing that this system would require is a transaction
We need to tell the network that the owner of some bitcoin value has authorized the transfer of that value to another owner
How do we make a transaction in real life?
First, build transaction
Ask for his name, amount to send, fill in date, etc. 
Then I sign the check, making it valid for him and only him to deposit (transact, verify identity)
On the Internet?
We probably make an account on some website, hook up our bank account (establish identity)
Find the ID of the person I want to pay to, fill in amount (create transaction)
Send him the money (sign transaction)
The system tells my bank account to subtract that that amount 
The system adds that amount to his account
In these examples, who is verifying the identity? The banks.
Bitcoin?
“We define an electronic coin as a chain of digital signatures” 
“Each owner transfers the coin to the next by digitally signing a hash of the previous transaction and the public key of the next owner and adding these to the end of the coin” - what the hell does this mean?
Before we go on, quick crypto lesson:
Hash Function:
Key/value pair… some functions takes a key in as an argument, spits out the value associated with this key
Cryptographic Hash Function:
Same idea, but has three important properties:
It is extremely easy to calculate a hash for any given data.
So it is very easy to verify the output/digest if we know the input/key
It is extremely computationally difficult to calculate an alphanumeric text that has a given hash.
One-way function… knowing the output does not mean we know the input… actually computationally difficult to know that 
It is extremely unlikely that two slightly different messages will have the same hash.
Collision resistant… all inputs will generate a unique output
Public/Private Keys and Bitcoin Addresses
Can think of pubKey as bank account number and privKey as your password/pin
Public/Private Key pairs are used to establish identity
Private keys are randomly generated 
Private keys are not stored in bitcoin network, stored by users in a file.. the keys are completely independent from the bitcoin protocol
Public keys are derived from private keys using Elliptic Curve multiplication (one-way) (ECDSA)...
Bitcoin address are derived from public keys


Digital Signatures
Is a mathematical scheme consisting of two parts:
First: an algorithm for creating a signature using a private key from a message (the transaction)
Second: an algorithm that allows anyone to verify the signature, given the message and the signer’s public key
Example:
Alice sends Bob 1btc, she signs the transaction message with her private key to generate her signature
Sign(“Alice to Bob: 1btc”, privateKeyAlice) = signatureAlice 
Anyone can verify that it was indeed Alice who signed it by running the signature and message against her public key
Verify(“Alice pays Bob: 1btc”, signatureAlice, publicKeyAlice) = True/False
So now we have a way to prove that Alice and only Alice can send money to Bob and that anyone can verify it with her public key and signature
AKA: we have a way to 
1) establish identity, prove that the owner of the private key (owner of the funds), has authorized the spending of those funds (signing)
2) prove that this authorization is undeniable (anyone with the owner’s public key and transaction hash can verify)
3) proves that the transaction have not and cannot be modified by anyone after it has been signed
But we need a way for the payee to ensure that the payer has not already signed any earlier transactions
Ex: Alice can sign a transaction saying “Alice pays Bob: 1btc”, then also sign a transaction saying “Alice pays Charles: 1btc”


Timestamp Server
Double spend problem:
Bank solves it by keeping a record of all transactions, and blocking anyone who tries to spend more than they have
We don’t have the privilege of a single group making decisions
So what to do?




Proof-of-Work
Network
Incentive
Reclaiming Disk Space
Simplified Payment Verification
Combining and Splitting Value
Privacy
Example of 51% Attack




Introduction
Purpose of this workshop isn’t to sell you guys on btc, or to discuss where btc gets value, more just to demystify the workings behind btc 
We will mostly be following the structure of the white paper
We can gather two things from just the title: an Electronic Cash System
Bitcoin is a “Cash System”
It is not simply a currency
It’s a protocol, a set of rules that user must follow in order to participate
With physical money, we can transfer money without a third party
I could simply hand Yon $10 and have that be it
But the problem with electronic money is that traditionally it has always required some third party to maintain trust throughout the transaction… 
… and in the event that there is some dispute, this party would be responsible for mediating it 
This model leads to two main issues:	
The third party would require a large amount of KYC to keep the customers accountable (bank account #, social security, etc)
The transaction costs would rise to keep the third party incentivized to keep providing their service
So by combining the use of cryptographic proofs and incentives, Bitcoin allows two parties to make secure, indisputable transactions directly to each other without some trusted third party
Transactions
“I have 1btc and I want to send it to Chris…”
Start off by drawing a chain of blocks, explain blockchain visually in big picture
“What does it mean to own 1btc? What does it look like on this chain?”
Having 1btc is not like having a dollar in your pocket or a dollar in your bank account
A “coin” is a chain of digital signatures… with each owner transferring the coin to the next person…
You could roughly imagine a bill in an envelope with covered in signatures and street addresses of everyone who has previously spent it and delivered it to the next person
Draw out chain of re-assigning ownership of a coin from Alice -> Bob -> Chris -> so on… 
How does this work in Bitcoin? How do I “get” a bitcoin? 
Crypto background
Hash Functions/Cryptographic Hash Functions
Asymmetric Encryption
Pub/priv key, signatures background
Draw out example of sending someone a message and how they would be able to see it
Each person has a pub/priv key pair
Everyone can know your public key
Only you can know the private key
Move to input | output
Someone has assigned this coin to me with my public key
For me to claim it, I need to prove that I own that key
How do I send a coin to someone?
Output with their public key
Double-spend problem
Could potentially assign ownership of the same coin to multiple people
Draw out example of creating multiple transactions from the same input to multiple outputs (t0, t1, t2)
In order to address this, we need to be aware of all transactions that occur
Banks solve the problem simply with being the trusted authority, ability to deny a transaction
In Bitcoin, we don’t have help of central authority
Timestamp Server 
We must have a way for everyone to be aware of all the transactions and agree on the single history of the order in which they were received 
Introduce concept of time of the transactions
If we add a timestamp to the input for creating a transaction, then it means that the data must have existed at that moment, there is no other way to generate the hash with the same data for a different timestamp
We form order between the transactions by putting them into blocks and having the block include the hash of the previous block, by so doing, establishing relative order between blocks/transactions
Proof-of-Work
So now we have a chain of blocks that are linked and have transactions in them that establish order and everyone is aware of every transaction 
Who gets to create blocks? How do we agree which block is valid or not?
It would be impossible for every participant to personally create a block… the network would just be spammed with blocks, it becomes so clogged that it becomes difficult to agree on an ordering
We need a way for every participant in the network to reach an agreement and say that ‘this block of transactions is valid, we all agree on this’
What Satoshi proposes is the utilization of Proof-of-Work
What this does is say that in order to performing some operation, you must expend a certain amount of computational power (electricity AKA money) 
PoW was first used in HashCash in the 90s (which he cites in the whitepaper)
Require the machine to perform some computational challenge that is small enough that it is still cheap enough to send an email but too costly to spam the network
In Bitcoin, in order to create a block, an individual must successfully solve a computationally exhausting challenge, proving that they have put an amount of work into this, compelling everyone to accept it
Mechanics of PoW:
The brute-force puzzle
Remember the properties of a cryptographic hash function
Now let’s take the hash of our block header and say there must be some value (nonce), where if we concatenate it to our block hash and run it through a hashing function, it will produce an output with x amount of leading zeros
There is no better way to find this nonce than to brute-force every single value and check if it produces an answer with x amount of leading zeros
What this does is prove that the party that found the answer has put in ‘work’ to find the answer
This party did nothing else than expend computational power, brute-forcing the function until it has found the answer 
It is very easy to verify, anyone can take the announced answer
As long as the majority of the CPU power in the network is controlled by honest nodes, the honest chain will grow the fastest and outpace any competing chain
We follow the longest chain, the chain with the most ‘work’ put into it,
Run through example on board of chaining block headers together
Show that we use the previous block hash to generate the next one
Show that in order to modify a past block, an attacker would have to redo the proof-of-work of the block and all the blocks after it and then catch up to the most recent block and still maintain a lead
Network
So far we have:
a way to securely transfer ownership between coins 
a way to prevent double-spending of spent outputs
and a way for the network to agree on the order of transactions/blocks/history
Now, how do they all work together?
New transactions are broadcast to all nodes
Each node collects new transactions into a block
Each node works on finding a difficult PoW for its block
When a node finds the PoW, it broadcasts the block to all nodes
Nodes accept the blocks only if all transactions in it are valid and not already spent
Nodes express their acceptance of the block on creating the next block in the chain, using the hash of the accepted block as the previous hash


