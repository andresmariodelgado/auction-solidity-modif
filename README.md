# Auction in Solidity - Auction.sol

## File

This project contains a smart contract written in Solidity that implements a simple auction, with a defined base bid, fixed duration, partial withdrawal of deposits by non-winning bidders while the auction is active, and refund of all non-winning bids at the end of the auction. A persistent historical record of bidders is kept, along with the winner and bid amount.

- **AuctionModif1.sol**: Main contract that handles all the auction logic.

## Main Features

- Automatic auction start upon deployment (lasts 2 days, with a base bid of 1 ether).

- Registration of successive bids, only if they are at least 5% higher than the current one.

- Bidders history.

- Refund of accumulated funds (except the last winning bid).

- Event emissions (`NewOffer`, `AuctionEnded`).

## Restrictions and Modifiers

- `onlyOwner`: Only the contract owner can execute the refund after the auction ends.

- `activeAuction`: Ensures the auction has not ended.

- `validprecio`: Validates that a new bid is higher than the current one.

## Key Structures and Variables

- `Bidders[] offerList`: Bid history with address and value.

- `mapping(address => uint256) acummOfers`: Accumulated amount per bidder.

- `keyList[]`: Unique key list for iteration.

- `event NewOffer`: Notifies new bids.

- `event AuctionEnded`: Notifies auction closure.

## Refund Logic and Discount

- Only the auction owner can refund the accumulated funds to all non-winning bidders (excluding the winner).

- A 2% fee is deducted from each refund, which remains in the contract.

- The winner does not receive a refund of their final bid, nor any earlier bids not withdrawn during the active auction.

## Function Analysis

**Function:** `bid`

- **Parameters:** None

- **Returns:** `Bidders[] memory`

- **Visibility:** external

- **Mutability:** payable

- **Description:** Registers a new bid. Can only be called if the auction is still active and the new bid is at least 5% higher than the current one. Updates the current winner, accumulates the bid value, and emits a `NewOffer` event.

**Function:** `withdrawalPartial`

- **Parameters:** None

- **Returns:** None

- **Visibility:** external

- **Description:** Allows a bidder to partially withdraw their accumulated amount, excluding their last bid.

**Function:** `showOfferList`

- **Parameters:** None

- **Returns:** `Bidders[] memory`

- **Visibility:** external

- **Description:** Displays an array of structures containing each bidder and their bid amount.

**Function:** `showWinner`

- **Parameters:** None

- **Returns:** `address` and `uint256`

- **Visibility:** external

- **Description:** Displays the winning bidder and their winning bid.

**Function:** `refund`

- **Parameters:** None

- **Returns:** None

- **Description:** Refunds, except to the winner, the bids not yet withdrawn, with a 2% fee kept in the contract. Only the contract owner can execute this function.

---

_Developed by Andrés Delgado for educational and exploratory purposes in the blockchain and decentralized auction space._