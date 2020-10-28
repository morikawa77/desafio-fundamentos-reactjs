<img alt="GoStack" src=".github/header-desafios-new.png" style="width: 100%;"/>

<h3 align="center">
  Challenge 05: First project Node.js
</h3>

<p align="center">
  <img alt="License" src="https://img.shields.io/static/v1?label=license&message=MIT&color=15C3D6&labelColor=000000">
</p>

### 🚀 About the challenge

In this challenge, you must continue to develop the transaction management application, training what you have learned so far in Node.js together with TypeScript, but this time including using a database with TypeORM and sending files with Multer!

This will be an application that should store incoming and outgoing financial transactions and allow the registration and listing of these transactions, in addition to allowing the creation of new records in the database by sending a csv file.

### ➡️ Application Routes

- **`POST /transactions`**: The route must receive title, value, type, and category within the body of the request, type being the type of the transaction, which must be income for incoming (deposits) and outcome for exiting (withdrawing). When registering a new transaction, it must be stored within your database, having the fields id, title, value, type, category_id, created_at, updated_at.

```json
{
  "id": "uuid",
  "title": "Salário",
  "value": 3000,
  "type": "income",
  "category": "Alimentação"
}
```

- **`GET /transactions`**: This route should return a listing of all the transactions you have registered so far, along with the sum of the entries, withdrawals and total credit. This route must return an object in the following format:
```json
{
  "transactions": [
    {
      "id": "uuid",
      "title": "Salário",
      "value": 4000,
      "type": "income",
      "category": {
        "id": "uuid",
        "title": "Salary",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Freela",
      "value": 2000,
      "type": "income",
      "category": {
        "id": "uuid",
        "title": "Others",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Pagamento da fatura",
      "value": 4000,
      "type": "outcome",
      "category": {
        "id": "uuid",
        "title": "Others",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Cadeira Gamer",
      "value": 1200,
      "type": "outcome",
      "category": {
        "id": "uuid",
        "title": "Recreation",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    }
  ],
  "balance": {
    "income": 6000,
    "outcome": 5200,
    "total": 800
  }
}
```

- **`DELETE /transactions/:id`**: The route must delete a transaction with the id present in the route parameters;

- **`POST /transactions/import`**: The route should allow the import of a .csv format file containing the same information needed to create a transaction id, title, value, type, category_id, created_at, updated_at, where each line of the CSV file must be a new record for the database, and finally return all transactions that have been imported into your database. The csv file, must follow the following <a target="_blank" href=".github/import_template.csv">model</a>.


<strong>Insomnia App was used to test endpoints</strong><br>
<img alt="Insomnia" title="Insomnia" src=".github/insomnia-preview-create.png" />
<img alt="Insomnia" title="Insomnia" src=".github/insomnia-preview-list.png" />
<img alt="Insomnia" title="Insomnia" src=".github/insomnia-preview-delete.png" />
<img alt="Insomnia" title="Insomnia" src=".github/insomnia-preview-import.png" />


<a target="_blank" href=".github/insomnia_transactions.json">Download Insomnia Endpoints JSON</a>

[![Run in Insomnia}](https://insomnia.rest/images/run.svg)](https://insomnia.rest/run/?label=Transactions&uri=https%3A%2F%2Fgist.githubusercontent.com%2Fmorikawa77%2F8d02ff1ac18f5e1afc2e923ff689762b%2Fraw%2Fd2a660efe2819195695a44dd8f4815d3517b2e2b%2Finsomnia_transactions.json)

<a target="_blank" href="https://www.notion.so/Rocketseat-Importando-arquivos-CSV-com-Node-js-50d34b9f6e55473baac41647fc85192f">Importing CSV files with nodejs</a>



### Tests Specification
⚠️ Before running the tests, create a database with the name "gostack_desafio06_tests" so that all tests can run correctly ⚠️

- **`should be able to create a new transaction`**: For this test to pass, your application must allow a transaction to be created, and return a json with the created transaction.

- **`should create tags when inserting new transactions`**: For this test to pass, your application must allow that when creating a new transaction with a category that does not exist, it is created and inserted in the category_id field of the transaction with the id that was just created.

- **`should not create tags when they already exists`**: For this test to pass, your application must allow that when creating a new transaction with a category that already exists, it is assigned to the category_id field of the transaction with the id of that existing category, not allowing the creation of categories with the same `title`.

- **`should be able to list the transactions`**: For this test to pass, your application must allow an array of objects to be returned containing all transactions along with the balance of income, outcome and total transactions that have been created so far.

- **`should not be able to create outcome transaction without a valid balance`**: In order for this test to pass, your application must not allow an outcome type transaction to exceed the total amount the user has in cash (total income), returning a response with HTTP 400 code and an error message in the following format: ````json{ error: string}````.

- **`should be able to delete a transaction`**: FFor this test to pass, you must allow your delete route to delete a transaction, and when you delete it, it returns an empty response, with status 204.

- **`should be able to import transactions`**: For this test to pass, your application must allow a csv file to be imported, containing the following <a target="_blank" href=".github/import_template.csv">model</a>. With the imported file, you must allow all records and categories that were present in that file to be created in the database, and return all transactions that were imported.

---

Made with ❤️ by morikawa77
