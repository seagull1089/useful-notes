* To create a simple project
```
mvn -B archetype:generate \
  -DarchetypeGroupId=org.apache.maven.archetypes \
  -DgroupId=com.mycompany.app \
  -DartifactId=my-app
```
* To download an artifact to local repository e.g
```
mvn dependency:get  -Dartifact=org.apache.httpcomponents:httpclient:4.5.2
```
