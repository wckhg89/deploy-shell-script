# deploy-shell-script
자바 jar 패키지 배포 스크립트 연습


```bash

#/!bin/bash

SET_NUM=$1
JAR_LOCATION=~/dev/www/$SET_NUM/my-slipp-$SET_NUM.war
SET1_OPTION=-Dserver.port=8080
SET2_OPTION=-Dserver.port=8081


SET1_PID=`jps | grep my-slipp-set1 | awk '{print $1}'`
SET2_PID=`jps | grep my-slipp-set2 | awk '{print $1}'`


if [ "$SET_NUM" = "set1" ]
then
  if [[ "" !=  "$SET1_PID" ]]; then
    echo "killing $SET1_PID"
    kill -9 $SET1_PID
  fi

  echo 'set1 run on 8080'
  java -jar $SET1_OPTION $JAR_LOCATION > ~/dev/www/nohup_set1.out &
elif [ "$SET_NUM" = "set2" ]
then
  if [[ "" !=  "$SET2_PID" ]]; then
    echo "killing $SET2_PID"
    kill -9 $SET2_PID
  fi

  echo 'set2 run on 8081'
  java -jar $SET2_OPTION $JAR_LOCATION > ~/dev/www/nohup_set2.out &
else
  echo 'CommandLine argument must be set1 or set2'
fi

```
