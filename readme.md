# GlobalMentor Root POM

Root POM for GlobalMentor projects. Provides profiles and dependency management for project building and testing.

Note that by default the `release` profile signs the artifact with the GlobalMentor software signing key during the `verify` phase. If verifying, installing, or deploying with the `release` profile in a non-GlobalMentor project, the key needs to be changed by overriding the `gpg.keyname` user property, or setting the `keyname` configuration of the [Apache Maven GPG Plugin](https://maven.apache.org/plugins/maven-gpg-plugin/) [`gpg:sign`](https://maven.apache.org/plugins/maven-gpg-plugin/sign-mojo.html) goal.

## Issues

Issues tracked by [JIRA](https://globalmentor.atlassian.net/projects/JAVA).

## Checking for Dependency/Plugin Updates

This POM allows you to check for newer dependencies and plugins available on Maven Central.

```bash
mvn versions:display-dependency-updates
mvn versions:display-plugin-updates
```

This POM is configured not to list non-release versions when checking for newer versions. Below are some real-world examples of non-release artifact versions that are ignored:

* `org.slf4j:slf4j-api:2.0.0-alpha7`
* `jakarta.enterprise:jakarta.enterprise.lang-model:4.1.0.Alpha1`
* `jakarta.persistence:jakarta.persistence-api:3.2.0-B01`
* `maven-surefire-plugin:3.0.0-M7`
* `jakarta.inject:jakarta.inject-api:2.0.1.MR`
