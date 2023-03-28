# Examples for hello / sh and artifacts plugin 



## Example 1 - single lines sh 

```
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                echo 'good good'
                sh 'pwd'
                sh 'ls -la'
                sh 'ls -la > test.txt'
                archiveArtifacts artifacts: 'test.txt', followSymlinks: false
            }
        }
    }
}

```

## Example 2: Multiple lines sh 

  * Question: Is file still available in next stage ?

```

pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                echo 'good good'
                sh '''
                  pwd
                  ls -la
                  ls -la > test.txt
                '''
                archiveArtifacts artifacts: 'test.txt', followSymlinks: false
            }
        }
        
        stage('Checker') {
            steps {
              sh 'ls -la'
            }
        }
    }
}


```

## Example 2: Multiple lines sh 

  * Question: Is file still available in next stage ?

```

pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                echo 'good good'
                sh '''
                  pwd
                  ls -la
                  ls -la > test.txt
                '''
                
            }
        }
        
        stage('Checker') {
            steps {
              sh 'ls -la'
            }
        }
        
        stage('Archiver') {
            steps {
              archiveArtifacts artifacts: 'test.txt', followSymlinks: false
            }
        }
        
    }
}


```

