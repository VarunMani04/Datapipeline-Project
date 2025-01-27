---
title: "Automated Podcast Pipeline Documentation"
author: "Data Engineering Project"
date: "`r format(Sys.time(), '%d %B, %Y')`"
output: 
  html_document:
    toc: true
    toc_float: true
    theme: cosmo
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Project Overview

An Apache Airflow DAG that automates the process of downloading and processing podcast episodes from Marketplace Tech. The pipeline handles XML feed parsing, episode storage in SQLite, and audio file downloads.

## Pipeline Components

### DAG Configuration
```{python dag-config, eval=FALSE}
@dag(
    start_date = pendulum.datetime(2023,9,1),
    dag_id = "podcast_summary",
    schedule_interval = "@daily",
    catchup = False
)
```

### Database Schema
```{sql schema, eval=FALSE}
CREATE TABLE IF NOT EXISTS episodes (
    link TEXT PRIMARY KEY,
    title TEXT,
    filename TEXT,
    published TEXT,
    description TEXT,
    transcript TEXT
);
```

### Key Features

* XML feed parsing using `xmltodict`
* SQLite database integration
* Duplicate episode detection
* Automated MP3 file downloads
* Daily scheduled execution

## Pipeline Tasks

1. **Database Creation**
   * Creates SQLite table if not exists
   * Handles podcast episode metadata

2. **Podcast Data Fetching**
   * Downloads XML feed
   * Parses episode information
   * Returns structured episode data

3. **Episode Processing**
   * Checks for existing episodes
   * Stores new episode metadata
   * Downloads audio files

## Dependencies

```{python dependencies, eval=FALSE}
from airflow.decorators import dag, task
from airflow.providers.sqlite.operators.sqlite import SqliteOperator
from airflow.providers.sqlite.hooks.sqlite import SqliteHook
import pendulum
import requests
import xmltodict
import os
```

## Task Flow

```{r task-flow, eval=FALSE}
# Task sequence visualization
create_database >> get_podcasts >> load_episodes >> download_episodes
```

## Usage

1. Configure Airflow connection for SQLite
2. Set podcast feed URL
3. Deploy DAG
4. Monitor execution in Airflow UI

## Error Handling

* Duplicate episode detection
* Database connection management
* File system operations

---
