# GlobalMentor Root POM

Root POM for GlobalMentor projects. Provides profiles and dependency management for project building and testing.

Note that by default the `release` profile signs the artifact with the GlobalMentor software signing key during the `verify` phase. If verifying, installing, or deploying with the `release` profile in a non-GlobalMentor project, the key needs to be changed by overriding the `gpg.keyname` user property, or setting the `keyname` configuration of the [Apache Maven GPG Plugin](https://maven.apache.org/plugins/maven-gpg-plugin/) [`gpg:sign`](https://maven.apache.org/plugins/maven-gpg-plugin/sign-mojo.html) goal.

## Publishing to Maven Central

Publishing to Maven Central uses the [Central Publishing Maven Plugin](https://central.sonatype.org/publish/publish-portal-maven/) and requires opt-in via the `central.publishing.enabled` property.

### Prerequisites

1. Create a [Portal User Token](https://central.sonatype.org/publish/generate-portal-token/) in the Sonatype Central Portal
2. Add the token to your Maven `settings.xml`:
   ```xml
   <servers>
     <server>
       <id>central</id>
       <username>your-token-username</username>
       <password>your-token-password</password>
     </server>
   </servers>
   ```

### Publishing Child Projects

To enable publishing for a child project, add to its POM:

```xml
<properties>
  <central.publishing.enabled>true</central.publishing.enabled>
</properties>
```

Then deploy with the `publish` profile:

```bash
mvn clean deploy -Ppublish
```

### Publishing the Root POM

To publish the root POM itself, enable publishing via command line:

```bash
mvn clean deploy -Ppublish -Dcentral.publishing.enabled=true
```

### Security Note

By default, `central.publishing.enabled` is `false` to prevent accidental publishing of proprietary projects. Projects must explicitly opt-in to publishing.

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
* `com.fasterxml.jackson.core:jackson-core:2.16.0-rc1`

