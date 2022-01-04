# Testing maven revision info with flatten-maven-plugin

```shell
mvn -Dmaven.test.skip=true -Dmaven.javadoc.failOnError=false --batch-mode release:clean release:prepare release:stage
```

```shell
export RELEASE_VER=$(cat revision.txt)
mvn ci-friendly-flatten:scmTag -Drevision=$RELEASE_VER
```


## References
* [Testing Maven Release Plugin Auto-Increment Version Number](https://www.javacodegeeks.com/2020/02/testing-maven-release-plugin-auto-increment-version-number.html)
* [Ci friendly versions of Maven multi module unified version management - ${revision}](https://cdmana.com/2021/03/20210308060558968h.html)
