<h1 align="center">Reelo Backend Task 🧭</h1>

## 📚 | Problem Statement

- Design and implement a Question Paper Generator application

- The application must store a number of questions in a Question Store. A question can have the following attributes {question, subject, topic, difficulty, marks}

  <aside> 💡 `{“What is the speed of light”, “Physics”, “Waves”, “Easy”, 5}`

</aside>

- The Question paper Generator should look for questions in the Question Store and then generate the question paper based on the total marks and the distribution of marks based on _Difficulty_



## 🎯 | Sample Queries

Assume the below requirement for a question paper:

> (100 marks, Difficulty, {20% Easy, 50% Medium, 30% Hard })

The problem statement here is that you need to generate a question paper of 100 marks total of which 20% (ie, 20 marks) worth of questions should have the _Difficulty_=Easy, 50% having _Difficulty_=Medium and 30% having _Difficulty_=Hard

## 🌐 | Test Project

- Clone this repository.
- Install Docker Desktop.
- Create a `.env` file in the root directory of the web-server folder with credentials `MONGODB_URI=mongodb://localhost:27017/question_paper`
- Run `docker-compose build` in the root directory of the project. This process takes a a minute or two to complete, for the first time.
- Run `docker-compose up --scale web-server=3` to initialize 3 load balanced web servers running on port 3000 to handle failovers.
- Hit up a get request on `http://localhost:3000/api/` to connect to DB and load test data.
- Hit up a get request on route `http://localhost:3000/api/getPaper` with json body              `{
  "totalMarks":50,
  "Easy":0,
  "Medium":60,
  "Hard":40
}` to the generate a test paper.

<br/>

## 📝 | System Design

<p align = center>
    <img alt="Project Logo" src="https://github.com/BREACH1247/Reelo-Paper-Generator/blob/eedc65b28d04365b1f0ec94ca33ca752e528886a/assets/Reelo%20System%20Design.png" target="_blank" />
</p>

### Features Implemented:

- The web-service is Load Balanced to avoid failover.

### Current Architecture:

- Containerized approach to solving the problem statement.
- Given the **non-blocking** & **async I/O** of **FastAPI**, it is used as the web framework. This will help in ingesting logs at a faster rate.
- **Apache Kafka** is used as the message broker. It will help in decoupling the ingestion and querying process.
- **Apache Cassandra** is used as the database. It is a NoSQL database and is highly scalable. It will help in storing the logs in a **distributed** manner. It also provides a fast read/write speed, i.e. **high throughput**.
- Query interface is built upon **Elasticsearch**. It is a distributed, RESTful search and analytics engine. It helps in providing a fast search result. Elasticsearch works wonders with large databases, with **high processing speeds**.
- The logs are ingested via an HTTP server, which runs on port `3000` by default.

### Future Scope:

- The current architecture is a very basic implementation of the problem statement.
- Depending upon the scale, the entire architecture can be **scaled horizontally**.
- Load Balancing can be implemented to handle high volumes of logs efficiently. We might use **AWS ELB**.
- **Apache Flink** can be setup between Kafka and Cassandra for streaming, processing and analytics.
- **Cassandra** can be used as a Data Lake, and **Apache Spark** can be used for analytics.
- **JWT Authentication** can be implemented for the Web UI. (didn't have time)
- **Regex filters** can be implemented on Elasticsearch. (didn't have time)

## 🧑🏽 | Author

**Aditya Sinha**

- Linkedin: [@AdityaSinha](https://www.linkedin.com/in/aditya-s-a07a54121/)
- Github: [@BREACH1247](https://github.com/BREACH1247)

<br/>

---