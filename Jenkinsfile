pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    environment {
    def TAG_EXIST = ""
    
    def LAST_TAG = ""
    def NEW_COMMITS = ""
    def NEW_TAG = ""
    def NEW_BRANCH = ""
    }
    stages {
        stage('Add tag') { 
            steps {
                script {
                sh "set +e"
                TAG_EXIST = sh(returnStdout: true, script: 'git rev-parse "v0.1" || echo "tags not found"').trim()
                TAG_EXIST = TAG_EXIST.substring(0,4);
                echo "$TAG_EXIST"
                if (TAG_EXIST != 'v0.1') {
                    echo "tag exist, commit $TAG_EXIST";
                    LAST_TAG = sh(returnStdout: true, script: 'git describe --tags --abbrev=0').trim();
                    NEW_COMMITS = sh(script: "git rev-list $LAST_TAG..HEAD --count", returnStdout: true)
                    echo "$NEW_COMMITS"
                    if (NEW_COMMITS != '0') {
                        echo "here"
                        
                        echo "here"
                        NEW_TAG = "${Float.parseFloat(LAST_TAG.substring(1)) + 0.1}"
                        NEW_TAG = NEW_TAG.substring(0, 3);
                        echo "$NEW_TAG"
                        echo "here"
                        NEW_BRANCH = "${Float.parseFloat(LAST_TAG.substring(1)) + 0.2}"
                        NEW_BRANCH = NEW_BRANCH.substring(0, 3);
                        echo "here"
                        sh "git tag v$NEW_TAG"
                        sh "git checkout -b v$NEW_BRANCH-rc1"
                    }
                } else {
                    echo "new tag";
                    sh "git tag v0.1"
                    sh "git checkout -b v0.2-rc1"
                }
                sh "git push origin --all"
                sh "git push origin --tags"
                }
            }
        }
    }
}
