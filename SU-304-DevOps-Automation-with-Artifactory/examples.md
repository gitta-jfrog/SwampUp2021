##REST API AUTOMATION

```bash
#!/bin/sh
FILE=list.txt
TOTAL=`cat $FILE | wc -l`
while read LINE
 do
   echo $TOTAL left
   # first we will try to download the file. if we can't download it, only then we will remove it. To actually run the deletions, remove the comments below.
   response=$(curl --write-out %{http_code} --silent --output /dev/null -uUSER:PASS -L https://ARTIFACTORY.COM/artifactory/${LINE})
   echo $response
   if [ "$response" -ne "200" ];
   then
     echo "${LINE} responded ${response}"
     # echo "deleting ${LINE}"
     # curl -uUSER:PASS -L -XDELETE https://ARTIFACTORY.COM/artifactory/${LINE}
   fi;
   TOTAL=`expr $TOTAL - 1`
done < $FILE
```


REST API LOOP:
```bash
#!/bin/bash
for i in {1..10000}
do
   curl -uadmin:password -H "Content-Type: application/json" -H "Accept: application/json"  -XPUT https://artifactory.yardeng.support-testlab.com/artifactory/api/security/users/myuser$i -d '{
  "name": "myuser'${i}'",
  "email": "user@jfrog.com",
  "password": "Qwer1234"
}'
done
```
