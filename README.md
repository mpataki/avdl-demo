# avdl-demo

This repo is intended to demonstrate an issue with the [maven-avro-schema-plugin](https://github.com/zolyfarkas/spf4j/tree/master/spf4j-avro-components/maven-avro-schema-plugin), pertaining to https://github.com/zolyfarkas/spf4j/issues/43.

Running `mvn clean compile` as is will genarate the following error:

```
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.823 s
[INFO] Finished at: 2020-04-07T11:44:28-04:00
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.spf4j:maven-avro-schema-plugin:8.8.0:avro-compile (default-avro-compile) on project avdl-demo: cannot add mvnId to  IDL /home/mat/code/avdl-demo/src/main/avro/A.avdl, Unable to resolve com.example.avro.timestamp_ms -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoExecutionException
```

But if you comment out the `maven-avro-schema-plugin` from the pom.xml, and uncomment the `avro-maven-plugin`, you'll see the project build successfully.

The issue seems to center around the use of `timestamp_ms` as a type in avdl. This is a logical type that Avro IDL itself does support, [as stated in their documentation](https://avro.apache.org/docs/current/idl.html).
