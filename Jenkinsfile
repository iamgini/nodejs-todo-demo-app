pipeline {
    agent any

    environment {
        // Git Repo
        GIT_URL = "https://github.com/ginigangadharan/nodejs-todo-demo-app"
        // Database variables
        DATABASE_SERVER = "dbnode1"
        POSTGRES_USER = "postgres"
        POSTGRES_PASSWORD = "PassWord"
        POSTGRES_DATABASE = "app2_db"
        POSTGRES_TABLE = "data_table"
        POSTGRES_NEW_USER_NAME = "devteam"
        POSTGRES_NEW_USER_PASSWORD = "DevPassword"
    }

    stages {
        stage ('Git Checkout') {
          steps {
              git branch: 'main', url: 'https://github.com/ginigangadharan/nodejs-todo-demo-app.git'
            }
        }
      
        stage("Build") {
            steps {
                echo "Include your build steps here"
            }
        }

        stage("Unit Test") {
            steps {
                script {
                    echo "Include your scanning and test tasks here"
                }
            }
        }

        stage("Integration Test") {
            steps {
                script {
                    echo "Integration Test"
                }
            }
        }

        stage("Creating Database") {
            steps {
                echo "Create database and user access using Ansible Automation Controller"
                script {
                    // Trigger Ansible controller job
                    //deploy('hello','prod');
                    ansible_controller_db_job();
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "Include tasks for deploying application"
                
            }
        }        
    }
}

def ansible_controller_db_job(){

     ansibleTower(
            towerServer: 'AAP-Demo',
            templateType: 'job',
            jobTemplate: 'PostgreSQL - Create Database and User Access',
            importTowerLogs: true,
            inventory: 'Ansible Dev Lab',
            jobTags: '',
            skipJobTags: '',
            limit: '',
            removeColor: false,
            verbose: true,
            credential: '',
            extraVars: '''---
            NODES: ["$DATABASE_SERVER"]
            postgres_user: "$POSTGRES_USER"
            postgres_password: "$POSTGRES_PASSWORD"
            postgres_database: "$POSTGRES_DATABASE"
            postgres_table: "$POSTGRES_TABLE"
            postgres_new_user_name: "$POSTGRES_NEW_USER_NAME"
            postgres_new_user_password: "$POSTGRES_NEW_USER_PASSWORD"
            '''
        )
}