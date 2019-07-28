pipeline {
    agent {
        label 'hemtt'
    }

    stages {
        stage('Build') {
            steps {
                bat 'hemtt build --release' 
            }
        }

        stage('Archive Build') {
            steps {
                archiveArtifacts artifacts: 'releases/**/*'
            }
        }

        stage('Publish to Steam Workshop') {
            when {
                branch 'master'
            }

            steps {
                publishSteamWorkshop '1817844401', 'releases/1.0.0/@anrop_unsung_jsrs', env.GIT_COMMIT
            }
        }
    }
}

void publishSteamWorkshop(String id, String mod, String changeNote) {
    bat "\"C:\\Program Files (x86)\\Steam\\SteamApps\\common\\Arma 3 Tools\\Publisher\\PublisherCmd.exe\" update /changeNote:$changeNote /id:$id /path:$mod"
}