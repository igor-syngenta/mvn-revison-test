# Testing maven revision info with flatten-maven-plugin

```shell
mvn -s ./.mvn/settings.xml clean package deploy ci-friendly-flatten:scmTag -Drevision=0.0.11 -Dchangelist=
 ```

This should show the produced settings from `build-helper-maven-plugin:parse-version` plugin execution:
```shell
mvn -s ./.mvn/settings.xml validate
```

Tagging git repository with `ci-friendly-flatten:scmTag`
```shell
export RELEASE_VER=$(cat revision.txt)
mvn -s ./.mvn/settings.xml clean package deploy ci-friendly-flatten:scmTag -Drevision=0.0.3 -Dchangelist=
```

## The problem
The big problem is to properly increase project version and commit it back to git repository. That would require some kind of maven plugin to work with `build-helper-maven-plugin:parse-version` to update the maven `revision` property in `pom.xml`.  
In the article [1](https://medium.com/javarevisited/how-to-increment-versions-for-maven-build-java-project-part-2-eefdebc53f5b) the author provides the solution with
`build-helper-maven-plugin:regex-property` but it does require a handful amount of plugin settings in the maven `pom.xml` project file. 

## Authorization

```shell
export CODEARTIFACT_TOKEN=`aws --region us-east-2 codeartifact get-authorization-token --domain cropwise-financials --domain-owner 500481770803 --query authorizationToken --output text`
```


## References
* [Testing Maven Release Plugin Auto-Increment Version Number](https://www.javacodegeeks.com/2020/02/testing-maven-release-plugin-auto-increment-version-number.html)
* [Ci friendly versions of Maven multi module unified version management - ${revision}](https://cdmana.com/2021/03/20210308060558968h.html)
* [Build Helper Maven Plugin: parse-version goal](https://www.mojohaus.org/build-helper-maven-plugin/parse-version-mojo.html)
* [How To Increment Versions For Maven Build Java Project — Part 1](https://medium.com/javarevisited/how-to-increment-versions-for-the-maven-build-java-project-a7596cc501c2)
* [How To Increment Versions For Maven Build Java Project — Part 2](https://medium.com/javarevisited/how-to-increment-versions-for-maven-build-java-project-part-2-eefdebc53f5b)
