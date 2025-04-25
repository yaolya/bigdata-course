## Big Data Analysis and Processing Technologies Course

### Run task
1. Clone this repository 
   ```bash
   git clone https://github.com/yaolya/bigdata-course.git
   cd bigdata-course
   ```
2. Start a [hadoop cluster](https://github.com/big-data-europe/docker-hadoop) 
    ```bash
    docker compose up -d
   ```
3. Run task (default TASK=h1)
   ```bash
   make wordcount TASK=h3
   ```


### Project Structure
```           
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

### Build with Ant
By default, tasks are built with Maven.
To build with Ant instead, add `lucene-analyzers-common-8.11.2.jar` and `lucene-core-8.11.2.jar` to the `h*/lib` directory of the task you're building, e.g. h2/lib, and run the task with:
```
make wordcount TASK=h2 BUILD_TOOL=ant
```
