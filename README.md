## Big Data Analysis and Processing Technologies Course
This repository contains a series of Hadoop MapReduce tasks.
To run these tasks on a different text, simply place your `.txt` files into the `resources/` directory.

##### h1: Word Frequency Count
Count word frequencies in a text using Lucene's standard analyzer, handling word delimiters and excluding stop words.

##### h2: Word Length Statistics
Modify the program from **h1** to count the number of words for each word length.
The output is a table where the key is the word length and the value is the number of words of that length.

##### h3: Most Frequent Next Word
Modify the program from **h1** to find, for each word, the most frequent word that follows it, treating punctuation as sentence boundaries.

### Prerequisites

- Java (JDK 8 or higher)

- Make

- Docker

- Maven or Ant

### Running a task
#### 1. Clone this repository 
   
   ```bash
   git clone https://github.com/yaolya/bigdata-course.git
   cd bigdata-course
   ```
#### 2. Start a [hadoop cluster](https://github.com/big-data-europe/docker-hadoop) 

```bash
    docker compose up -d
```
#### 3. Run task
To run a task (default `TASK=h1`):
   ```bash
   make wordcount TASK=h3
   ```

This command automates the full workflow for each task:
- Builds the selected task with **Maven** (default) or **Ant**.
- Builds a corresponding **Docker image**.
- Launches a container connected to the **Hadoop cluster**.
- Loads input files into **HDFS**.
- Runs the **Hadoop MapReduce** job.
- Copies the output results back to the local machine (`output/`).

##### Using Ant instead of Maven

By default, tasks are built with Maven.
To build with Ant instead, add `lucene-analyzers-common-8.11.2.jar` and `lucene-core-8.11.2.jar` to the `h*/lib` directory of the task you're building, e.g. `h2/lib`, and run the task with:
```bash
make wordcount TASK=h2 BUILD_TOOL=ant
```
This will build the h2 task with Ant and proceed with the same execution steps.

### Project Structure
```bash           
.
├── h*/                     # Folders: h1, h2, h3... for each task
│   ├── lib/                # JAR dependencies (for Ant)
│   ├── output/             # Job results
│   ├── src/                # Java source files
│   ├── pom.xml             # Maven build config
│   ├── build.xml           # Ant build config
│   └── build.properties
├── resources/              # Input files
├── scripts/
│   ├── hadoop-run-task.sh  # Run Hadoop JAR inside the container
│   └── hdfs-job-runner.sh  # Manage HDFS 
├── docker-compose.yml      # Start Hadoop cluster
├── hadoop.env              # Hadoop config variables
├── Dockerfile              # Build Hadoop job image
├── Makefile                # Build task + run Hadoop job
└── README.md

```
