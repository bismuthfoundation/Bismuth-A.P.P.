# APP-0001

Provide a way to link - both ways - a Twitter handle and a crypto address

## Why?

- Prove that you own a crypto account or a twitter account
- Opens the door to twitter operated bots, wallets, tipping
- Since contests and giveways are easy to flood with as many addresses as you want, limit fraud by requiring a linked social account in order to participate, can limit to 1 account. Reduce both crypto and twitter fraud by requiring that unique bond.
- Ease referals by having a referal code tied to the social account
- Allows to use the chain as a safe profile hub, certifying the legitimacy and connection of various social accounts.

## Pros and cons

Pros:
- Proves that the social account owner has private key to the crypto account
- proves that the crypto address owner wants to link to that social account
- public information to be used by anyone. Do it once, can be used by many service operators

Cons:
- Public information that is recorded forever.
- Needs some scraping/querying of the social media to link to.

## How

### General principle

- Sign your twitter handle, and publish its sha 256 hash
- Send a specific transaction from your wallet that includes your tweet id and the full signature

Using a sha256 hash allows for a constant size of the data to be tweeted, whatever the underlying crypto signature length is.

### The Protocol

Operation:  
`account:link`

Data:  
`twitter:id_of_the_tweet:full_signature_of_the_twitter_handle`

### Implementation guidelines

The trigger is a crypto transaction with a "account:link" operation meta field.

- account is the sender of the transaction
- get twitter handle and tweet content from `id_of_the_tweet`
- make sure the tweet exists
- check the signature validity, from twitter handle and `full_signature_of_the_twitter_handle`
- make sure sha256(full_signature_of_the_twitter_handle) is the tweet content (question: allow for more than just the sha?)

- store/cache the current association state.

## Possible extensions

- Generalize to other social meda accounts
- Allow "unlink" as well as "link"

- Design a private variation of this protocol
