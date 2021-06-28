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
### User
| Field       | Type        |
| :---:       | :---:       |
| id          | (Default)   |
| username    | (Default)   |
| password    | (Default)   |
| jaccount_id | BIGINT      |

### Classroom
Classroom is the same as `class` but avoid duplication of keywords in python.

| Field    | Type         |
| :---:    | :---:        |
| id       | (Default)    |
| name     | VARCHAR(256) |
| class_id | VARCHAR(20)  |
| owner(*) | user_id      |

**Note**: (`*`) means foreign key.

### Event
| Field           | Type         |
| :---:           | :---:        |
| id              | (Default)    |
| name            | VARCHAR(256) |
| expiration_date | datetime     |
| class_id(*)     | class_id     |
| booklist_id(*)  | booklist_id  |

### Invoice
| Field       | Type         |
| :---:       | :---:        |
| id          | (Default)    |
| user_id(*)  | user_id      |
| event_id(*) | event_id     |
| total       | DOUBLE       |
| status      | INT          |
| detail      | TEXT         | 

The value of status means:
- 0 : unpaid
- 1 : paid

`detail` is a json includes the count of books that the user want to buy.
It looks like this:
```json
[{
  "id": 1,
  "count": 100
}]
```

**Note**: We should make sure that each book in `detail` field is in the book_list
of the `Event`

## Contribution
### Collaborators
Collaborators should open an issue that describes the function/feature/bugs that 
to be added or fixed. 
Then the collaborator need to open a new branch and commit codes to that branch instead of `dev` or `main`.

The branch's name should reveal the function of codes, thus it should look like this:
- feat-add-book-with-permission
- fix-add-book-not-in-book-list
- docs-database-design-optimize

If you are not sure which name to use, please contact [@truc0](mailto:22969604+truc0@users.noreply.github.com) first.

### Others
The procedure for non collaborators' contribution is similar:
1. Open an issue describing the feature or fix you want
2. Collaborators will open a branch (called b1 in the following text) corresponding to the issue
3. Fork the project and make some change
4. submit a `Pull Request` to `b1`

If you are a student from `SJTU` and willing to contribute for a long time, please contact [@truc0](mailto:22969604+truc0@users.noreply.github.com)
and we may add you as a collaborator.
