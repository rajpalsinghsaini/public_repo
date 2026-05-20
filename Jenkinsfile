pipeline {
    agent any

     triggers {
        githubPush()
    }

    environment {
        REPO_NAME = "public_repo"
        REPO_URL  = "https://github.com/rajpalsinghsaini/public_repo.git"
        GIT_EMAIL = "[email protected]"
        GIT_NAME  = "Jenkins"
    }

    stages {

        stage('Clone Repository') {
            steps {

                script {

                    if (fileExists("${REPO_NAME}/.git")) {

                        echo "Repository already exists."

                    } else {

                        dir("${REPO_NAME}") {

                            git branch: 'main',
                                credentialsId: 'git-secret',
                                url: "${REPO_URL}"
                        }

                        echo "Repository cloned successfully."
                    }
                }
            }
        }

        stage('Make Changes') {
            steps {

                dir("${REPO_NAME}") {

                    sh '''
                        echo "Updated by Jenkins on $(date)" >> newfile2.txt
                    '''
                }
            }
        }

        stage('Commit and Push') {
            steps {

                dir("${REPO_NAME}") {

                    withCredentials([
                        usernamePassword(
                            credentialsId: 'git-secret',
                            usernameVariable: 'GIT_USERNAME',
                            passwordVariable: 'GIT_PASSWORD'
                        )
                    ]) {

                        sh '''
                            git config user.email "$GIT_EMAIL"
                            git config user.name "$GIT_NAME"

                            // git status

                            // git add .

                            // git diff --cached --quiet || git commit -m "Code pushed from Jenkins"

                            //git push https://$GIT_USERNAME:$GIT_PASSWORD@github.com/rajpalsinghsaini/public_repo.git main

                            git pull https://$GIT_USERNAME:$GIT_PASSWORD@github.com/rajpalsinghsaini/public_repo.git main
                        '''
                    }
                }
            }
        }
    }
}
