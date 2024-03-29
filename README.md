# Postman API tests project

This project contains Postman collections that were written for the endpoint from [opened swagger API](https://petstore.swagger.io/#/pet).
Test cases you can see [here](https://docs.google.com/spreadsheets/d/1SzCLbscloZAo2fhsyoqiJHQ-wTx0q3AGyApJEI4QF9s/edit?usp=sharing).
There are used Postman Sandbox API: JavaScript pre-request and tests scripts.  
A couple of tests realizes DDT techniques: test data are read from CSV or generated in pre-request script. Other test data are generated automatically and have random values.     
Postman collection can be launched using Newman from the console or Jenkins. Newman creates informative reports.   
Postman tests collection can be integrated into CI/CD.    

## Tools
Postman, Postman Sandbox API, JavaScript, Newman

## Usage

### How to run the project on Windows OS from the command line
* open command line
* check Node.js `node -v`
  * if Node.js doesn't find install version 8.X or 10.X from [Node.js](https://nodejs.org/en/)
* install Newman `npm install -g newman`
* clone git repository `https://github.com/MaryGeraseva/5-postman-api-tests.git`
* open project folder `cd 5-postman-api-tests`
* run test collection with newman `newman run [$collection-name.json] -d [$external-data-file.csv]`
  * as an example `newman run POST_200_with_post200data.postman_collection.json -d post200data.csv`
  * external data files have to use only with POST_200_with_post200data.postman_collection.json (post200data.csv) and 
  POST_400_with_post400data.postman_collection.json (post400data.csv)


### How to run the project with Jenkins
* open Jenkins and create pipeline job
* add in the section "Pipeline" script
![alt text](https://github.com/MaryGeraseva/screenshots/blob/master/pipeline.png)
  * on Linux:
```
pipeline {
    agent any
    stages {
        stage('download') {
            steps {
                 git 'https://github.com/MaryGeraseva/5-postman-api-tests.git'
                 sh 'npm install'
            }
        }
        stage('tests') {
            steps {
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run delete-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run get-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run get-all-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run post-get-delete-get-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run headers-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run nonexistent-endpoint-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run not-allowed-method-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run post-200-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run post-400-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run post-400-with-post400data-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                sh 'npm run post-200-with-post200data-tests'    
                }
            }
        }
    }
}
```
  * on Windows:
```
pipeline {
    agent any
    stages {
        stage('download') {
            steps {
                 git 'https://github.com/MaryGeraseva/5-postman-api-tests.git'
                 bat 'npm install'
            }
        }
        stage('tests') {
            steps {
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run delete-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run get-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run get-all-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run post-get-delete-get-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run headers-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run nonexistent-endpoint-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run not-allowed-method-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run post-200-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run post-400-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run post-400-with-post400data-tests'    
                }
                catchError(buildResult:'FAILURE', stageResult:'SUCCESS') {
                bat 'npm run post-200-with-post200data-tests'    
                }
            }
        }
    }
}
```
* safe and run job

### How to run the project with Jenkins and Jenkins-job-builder
Jenkins job builder is an additional application which takes simple descriptions of Jenkins jobs in YAML or JSON format and uses them to configure Jenkins.   
Jenkins job builder files for this project and usage information in my next [project](
https://github.com/MaryGeraseva/4-jenkins-job-builder.git).


### How to run the project with Postman desktop application
* open command line
* clone git repository `https://github.com/MaryGeraseva/5-postman-api-tests.git`
* import collections:  
open Postman --> on the toolbar push "Import" button --> "Import File" --> "Choose Files" --> import files from downloaded repository  

![alt text](https://github.com/MaryGeraseva/screenshots/blob/master/toolbar%20%201.png)

![alt text](https://github.com/MaryGeraseva/screenshots/blob/master/import.png)

* run tests with Postman Runner:   
on the toolbar push "Runner" button --> choose collection --> [optional] on the toolbar in section "Data" push "Select file" button--> run tests  

![alt text](https://github.com/MaryGeraseva/screenshots/blob/master/toolbar%20%202.png)

![alt text](https://github.com/MaryGeraseva/screenshots/blob/master/runner.png)   
  
a couple of collections have to run only with external data files:
POST_200_with_post200data.postman_collection.json with post200data.csv and
POST_400_with_post400data.postman_collection.json with post400data.csv


## For feedback
**e-mail:** mary.geraseva@gmail.com  
**telegram:** @MaryGeraseva  
**skype:** mary_geraseva  
[linkedIn](https://www.linkedin.com/in/maria-geraseva/)
