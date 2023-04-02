# Research: LangChain, Titanic SQLite Database, and the API of OpenAI

The main goal of this Jupyter Notebook is to use the Titanic SQLite database to explore the [LangChain](https://python.langchain.com/) library and the API of [OpenAI](https://openai.com/).

I'm using the [SQL Database Agent](https://python.langchain.com/en/latest/modules/agents/toolkits/examples/sql_database.html) of LangChain in order to interact with the database in a natural language way.

## Database

The table is called `titanic` and has the following columns.

🥳 Amazing: even the this table was created using natural language:

> "Give the column name, data type and description of the table titanic in markdown format"

| Column Name | Data Type | Description                           |
| ----------- | --------- | ------------------------------------- |
| PassengerId | TEXT      | Unique identifier for each passenger  |
| Survived    | TEXT      | Whether the passenger survived or not |
| Pclass      | TEXT      | Passenger class                       |
| Name        | TEXT      | Passenger name                        |
| Sex         | TEXT      | Passenger gender                      |
| Age         | TEXT      | Passenger age                         |
| SibSp       | TEXT      | Number of siblings/spouses aboard     |
| Parch       | TEXT      | Number of parents/children aboard     |
| Ticket      | TEXT      | Ticket number                         |
| Fare        | TEXT      | Ticket fare                           |
| Cabin       | TEXT      | Cabin number                          |
| Embarked    | TEXT      | Port of embarkation                   |

## Answering the questions with natural language

After the configuration the agent is able to answer the following questions:

1. How many passengers survived?
2. How many passengers were in each class?
3. How many passengers survived/died within each class?
4. What was the average age of survivors vs non-survivors?
5. What was the average age of each passenger class?
6. What was the average fare by passenger class? By survival?
7. How many siblings/spouses aboard on average, by passenger class? By survival?
8. How many parents/children aboard on average, by passenger class? By survival?

### Example #1: How many passengers survived?

```python
> Entering new SQLDatabaseChain chain...
How many passengers survived?

SQLQuery: SELECT COUNT(*) FROM titanic WHERE Survived = '1';

SQLResult: [(342,)]

Answer: 342 passengers survived.
> Finished chain.

' 342 passengers survived.'
```

### Example #2: How many passengers were in each class?

```python
> Entering new SQLDatabaseChain chain...
How many passengers were in each class?

SQLQuery: SELECT Pclass, COUNT(*) FROM titanic GROUP BY Pclass;

SQLResult: [('1', 216), ('2', 184), ('3', 491)]

Answer: There were 216 passengers in first class, 184 passengers in second class, and 491 passengers in third class.
> Finished chain.

' There were 216 passengers in first class, 184 passengers in second class, and 491 passengers in third class.'
```
