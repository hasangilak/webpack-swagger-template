use this shell script to simply build your code on top of yaml or json.


#webpack config
add this to your webpack config

```javascript
node: {
    fs: "empty"
}
```

#package dependency
install superagent
```shell
npm install --save superagent
```


use this shell to run the generator. check the shell variables first.
```shell
#!/bin/sh

SCRIPT="$0"

while [ -h "$SCRIPT" ] ; do
  ls=`ls -ld "$SCRIPT"`
  link=`expr "$ls" : '.*-> \(.*\)$'`
  if expr "$link" : '/.*' > /dev/null; then
    SCRIPT="$link"
  else
    SCRIPT=`dirname "$SCRIPT"`/"$link"
  fi
done

if [ ! -d "${APP_DIR}" ]; then
  APP_DIR=`dirname "$SCRIPT"`/..
  APP_DIR=`cd "${APP_DIR}"; pwd`
fi

executable="/home/user/work/swagger-codegen-cli.jar"

if [ ! -f "$executable" ]
then
  mvn clean package
fi

rm -rf /home/user/work/front-end/myproject/swagger/webpack-output

# if you've executed sbt assembly previously it will use that instead.
export JAVA_OPTS="${JAVA_OPTS} -Xmx1024M -DloggerPath=conf/log4j.properties"
ags="$@ generate -t /home/user/webpack-swagger-template
-i http://swagger.io/myproject.yaml
-l javascript -o /home/user/work/swagger/webpack-output"

java -DappName=PetstoreClient $JAVA_OPTS -jar $executable $ags

```
