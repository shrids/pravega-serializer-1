# Pravega Custom Serializers

Pravega Client (ref: https://github.com/pravega/pravega) currently implements `io.pravega.client.stream.impl.JavaSerializer` and `io.pravega.client.stream.impl.ByteArraySerializer`. It does not suppport other forms of serialization or enable serializers to enable compression as implementing them as part of Pravega Client would lead to forcing unwanted dependencies on the user application. 

To solve this pravega-serializer repository creates different gradle build targets to generate specific artifacts for serializers which depend on external dependencies. These specialized Pravega serializers depend on on a specific type of serializer thereby ensuring no unwanted transitive dependencies are forced on the user application.

## Project Structure

The project structure is described below.
```
pravega-serializer
   |---- json  (This supports Json based serializers)
   |---- avro 
   |---- customer serializers
```   
   Each sub module will generate a serailizer specific artifact which would depend on the pravaga-client and the specific external serializer libraries.
   
## Usage
Adding a dependency on a specific serializer by the user application in the build system like gradle / maven / ant.
e.g: `pravega-serailizer-json:x.y.z` will result in the pravega-client:x.y.z being downloaded as part of the transitive dependency along with the JSON serializer specific libraries.
