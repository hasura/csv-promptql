# AI Assistant on CSV Files

Supports importing multiple CSV files, each with their own schema.

## Pre-requisites

You'll need the Hasura CLI (authenticated via a Hasura account) and Docker installed on your local machine. Links to these steps are below:

- [Sign up for a Hasura account](https://console.hasura.io) (if you haven't)
- [Hasura CLI](https://hasura.io/docs/3.0/cli/installation) installed and authenticated
- [Docker](https://docs.docker.com/engine/install/) installed on your local machine

## Import your CSV Files

**Step 1: Clone the project**

```bash copy
git clone git@github.com:hasura/csv-promptql.git
cd csv-promptql
```

**Step 2: Configure CSV file(s)**

Place your CSV file(s) inside `app/connector/csv/csv_files` directory.

```bash copy
cd app/connector/csv/csv_files
```

Add your CSV files here.

**Step 3: Introspect the Connector**

```bash copy
ddn connector introspect csv
```

**Note**: Depending on how big the dataset is, it should take sometime to fully import the data. The schema will be initialized quickly and the data import happens in the background, so you can proceed to follow the steps below.

**Step 4: Add Models**

Based on the dataset imported, a SQL schema would be generated. Let's track all the models to get started quickly.

```bash copy
ddn model add csv "*"
```

## Build your PromptQL app

Now, let's set up the Hasura DDN project with PromptQL to start exploring the data in natural language!

- Set up the Hasura DDN project already scaffolded in the repo:

In the root directory of the repo, run the following commands:

```bash copy
ddn supergraph build local
ddn project init
```

- Start the DDN project

Let's start the DDN project by executing the following command:

```bash
ddn run docker-start
```

- Open the local DDN Console to start exploring:

```bash
ddn console --local
```

This should open up your browser (or print a browser URL) for displaying the Hasura Console. It’ll typically be something like: [https://console.hasura.io/local?engine=localhost:3280&promptql=localhost:3282](https://console.hasura.io/local?engine=localhost:3280&promptql=localhost:3282)

## Ask questions about your dataset

The app will have metadata about the dataset that you just imported above. You should be able to ask domain specific questions and play around with the data.

Here's a sample of what you can ask to get started.
- Hi, what can you do?

Depending on the dataset schema, PromptQL will tell you what it can answer and you can go from there.

## Clean up and restart your app

If you want to reset the data and start from scratch:

Modify or delete the csv files in the `app/connector/csv/csv_files` directory

You can stop the `ddn run docker-start` command, whereever it is running and you can execute the following in the root directory of the repo:

```bash copy
docker compose down -v && ddn run docker-start
```
