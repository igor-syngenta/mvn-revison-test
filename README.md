# Testing maven revision info with flatten-maven-plugin

```shell
mvn -s ./.mvn/settings.xml release:clean release:prepare release:perform --batch-mode -Dmaven.test.skip=true -Dmaven.javadoc.failOnError=false  
mvn -s ./.mvn/settings.xml release:clean release:prepare release:perform -B -DskipTests=true -Djava.security.egd=file:/dev/./urandom -Darguments="-Dmaven.javadoc.skip=true" -DscmCommentPrefix="[aws-codebuild] "
```

```shell
export RELEASE_VER=$(cat revision.txt)
mvn ci-friendly-flatten:scmTag -Drevision=$RELEASE_VER -Dchangelist=
```

## Authorization

```shell
export CODEARTIFACT_TOKEN=`aws --region us-east-2 codeartifact get-authorization-token --domain cropwise-financials --domain-owner 500481770803 --query authorizationToken --output text`
```


## References
* [Testing Maven Release Plugin Auto-Increment Version Number](https://www.javacodegeeks.com/2020/02/testing-maven-release-plugin-auto-increment-version-number.html)
* [Ci friendly versions of Maven multi module unified version management - ${revision}](https://cdmana.com/2021/03/20210308060558968h.html)
