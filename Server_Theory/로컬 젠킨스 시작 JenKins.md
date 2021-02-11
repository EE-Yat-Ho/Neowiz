로컬 젠킨스 시작
$ docker pull jenkins/jenkins:lts
$ docker run -d \
    -p 8080:8080 -p 50000:50000 \
    --name jenkins jenkins/jenkins:lts

brew services start jenkins-lts


73060625393a46268dd4778adc61ac0f
