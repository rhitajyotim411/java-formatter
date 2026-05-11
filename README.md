# Marionette Java Style

Shared Eclipse JDT formatter profile for Java projects.

The formatter profile lives at:

```text
eclipse-java-marionette-style.xml
```

## VS Code

After pushing this repository to GitHub, use the raw file URL in your VS Code
`settings.json`:

```json
{
  "java.format.settings.url": "https://raw.githubusercontent.com/<owner>/<repo>/main/eclipse-java-marionette-style.xml",
  "java.format.settings.profile": "MarionetteStyle"
}
```

Replace `<owner>` and `<repo>` with the GitHub owner and repository name.

If your default branch is not `main`, replace `main` in the URL with your branch
name.

VS Code does not need the XML file to be downloaded into each project. The Java
extension reads the formatter profile directly from the raw GitHub URL.

For this to work easily across machines, keep this repository public. A private
GitHub raw URL requires authentication, and putting personal access tokens in
`settings.json` is not recommended.

If the formatter must stay private, use a local file path or host the XML behind
an internal URL that every developer can access without embedding secrets in
project settings.

## Maven Spotless

Spotless uses a local formatter file path in the configuration below, so copy
`eclipse-java-marionette-style.xml` into the root of each Maven project that uses
this plugin setup.

Add this plugin under `plugins` in your `pom.xml`:

```xml
<plugin>
  <groupId>com.diffplug.spotless</groupId>
  <artifactId>spotless-maven-plugin</artifactId>
  <version>2.43.0</version>

  <configuration>
    <java>
      <eclipse>
        <file>${project.basedir}/eclipse-java-marionette-style.xml</file>
      </eclipse>
      <includes>
        <include>src/**/*.java</include>
      </includes>
    </java>
  </configuration>

  <executions>
    <execution>
      <goals>
        <goal>apply</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

Useful commands:

```sh
mvn spotless:apply
mvn spotless:check
mvn spotless:check -X
mvn spotless:apply -X
```

Command details:

- `mvn spotless:apply` formats matching Java files in place.
- `mvn spotless:check` checks whether matching Java files are formatted and
  fails the build if any file needs changes.
- `-X` enables Maven debug output. It can be used with either
  `spotless:check` or `spotless:apply`, for example `mvn spotless:apply -X`.
