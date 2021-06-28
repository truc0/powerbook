# Development Docs
This file describes the development procedure of [PowerBook](https://github/truc0/powerbook) project.

## Requirements
#### Normal User
Normal user can get `a list of books` which will be used in the next semester and choose which to purchase.
Normal users cannot change their choices after confirmation or `expiration date`.

An `Invoice` will be generated after a user confirm his/her choices, and they need to pay with a `QRCode` that
is uploaded by the `Manager/Owner` of the class. 
We recommend users enter the last 7 digit of the id of the trade record for better recognizing the relationship of
trade records and users.

Note that **only** class `Manager/Owner` can change the status of an invoice (`paid`/`unpaid`).

#### Manager / Owner
A class should have **only** 1 `Owner` and some managers.
Owners and managers have the same privileges but managing (add/remove) manager is owner exclusive.

Manager can:
- set up a `Event`(for book purchasing or something else)
- change the info of the `Event` (`expiration date`, etc.)
- change the status of `Invoice` (paid/unpaid)
- change the detail of `Invoice`
- download/know the summary of an `Event` (counts of books)

## Timeline
| Functions            | Time       | Status |
| :---:                | :---:      | :---:  |
| Development Docs     | 2021.06.30 |        |
| User Functions       | 2021.07.02 |        |
| Classroom Functions  | 2021.07.04 |        |
| Book & BookList      | 2021.07.06 |        |
| JAccount Integration | 2021.07.12 |        |

## Database Design
