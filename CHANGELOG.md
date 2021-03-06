## Change Log

# 1.4.1

- added `inputField` to both `TensorFlowServingTransform` and `HTTPTransform` to allow overriding default field `value`.
- added `ImageExtract` to read image files for machine learning etc.
- added the `minLength` and `maxLength` properties to the `string` metadata type.

# 1.4.0

- bump to Spark [2.4.0](https://spark.apache.org/releases/spark-release-2-4-0.html).
- bump to OpenJDK 8.181.13-r0 in `Dockerfile`.

# 1.3.1

- added additional tutorial job at `/tutorial/starter`.

# 1.3.0

- added support for dynamic runtime configuration via `Dynamic Configuration Plugins`.
- added support for custom stages via `Pipeline Stage Plugins`.
- added support for Spark SQL extensions via custom `User Defined Functions` registration.
- added support for specifying custom `formatters` for `TypingTransform` of integer, long, double and decimal types.
- added `failMode` for `TypingTransform` to allow either `permissive` or `failfast` mode.
- added `inputView` capability to `HTTPExtract` stage.

# 1.2.1

- bump to Spark [2.3.2](https://spark.apache.org/releases/spark-release-2-3-2.html).

# 1.2.0

- added support for Spark [Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html).
- added `pathView` property for `BytesExtract` allowing a dataframe of file paths to be provided to dynamically load files.
- added `TextExtract` to read basic text files.
- added `RateExtract` which wraps the Spark [Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html#creating-streaming-dataframes-and-streaming-datasets) rate source for testing streaming jobs.
- added `ConsoleLoad` which wraps the Spark [Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html#output-sinks) console sink for testing streaming jobs.
- added ability for `JDBCLoad` to execute in Spark [Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html#output-sinks) mode.

# 1.1.0

- fixed a bug in the `build.sbt` mergeStrategy which incorrectly excluded the `BinaryContentDataSource` registration when `assembly`.
- changed `TensorFlowServingTransform` to require a `responseType` argument.

# 1.0.9

- added the ability to add column level `metadata`.
- added the `MetadataFilterTransform` stage - a stage which allows filtering of columns by their metadata.
- added the `PipelineExecute` stage - a stage which allows embeding other pipelines.
- added the `HTTPTransform` stage - a stage which calls an external API and adds result to Dataframe.
- added support for Google Cloud Storage - prefix: `gs://`
- added support for Azure Data Lake Storage - prefix: `adl://`
- added `partitionColumn` to `JDBCExtract` to support parallel extract.
- added `predicates` to `JDBCExtract` to allow manual partition definitions.
- changed `XMLExtract` to be able to support reading `.zip` files.
- changed `*Extract` to allow input `glob` patterns not just simple `URI`.
- changed `*Extract` to support the schema to be provided as `schemaView`.
- added `BytesExtract` to allow `Array[Bytes]` to be read into a dataframe for things like calling external Machine Learning models.
- refactored `TensorFlowServingTransform` to call the `REST` API (in batches) which is easier due to library conflicts creating `protobuf`.
- create the `UDF` registration mechanism allowing logical extension point for common functions missing from Spark core.

# 1.0.8

- added the `KafkaLoad` stage - a stage which will write a dataset to a designated `topic` in Apache Kafka.
- added the `EXPERIMENTAL` `KafkaExtract` stage - a stage which will read from a designated `topic` in Apache Kafka and produce a dataset.
- added the `KafkaCommitExecute` stage - a stage which allows the commiting of the Kafka offsets to be deferred allowing quasi-transactional behaviour.
- added integration tests for `KafkaLoad` and `KafkaExtract`. more to come.
- added `partitionBy` to `*Extract`.
- added `contiguousIndex` option to file based `*Extract` which allows users to opt out of the expensive `_index` resolution from `_monotonically_increasing_id`.
- added ability to send a `POST` request with `body` in `HTTPExtract`.
- changed hashing function for `DiffTransform` and `EqualityValidate` from inbuilt `hash` to `sha2(512)`.

# 1.0.7

- added the `DiffTransform` stage - a stage which efficiently calculutes the difference between two datasets and produces left, right and intersection output views.
- added logging of `records` and `batches` counts to the `AzureEventHubsLoad`.
- updated the `EqualityValidate` to use the `hash` diffing function as the inbuilt `except` function is very difficult to use in practice. API unchanged.
- updated the `HTTPExecute` stage to not automatically split the response body by newline (`\n`) - this is more in line with expected usecase of REST API endpoints.

# 1.0.6

- updated `AzureEventHubsLoad` to use a SNAPSHOT compiled JAR in `/lib` to get latest changes. this will be changed back to Maven once version is officially released. Also exposed the expontential retry options to API.
- initial testing of a `.zip` reader/writer.

# 1.0.5

- fix a longstanding defect in `TypingTranform` not correctly passing through values which are already of correct type.
- change the `_index` field added to `*Extract` from `monotonically_increasing_id()` to a `row_number(monotonically_increasing_id())` so that the index aligns to underlying files and is more intuitive to use.

# 1.0.4

- allow passing of same metadata schema to `JSONExtract` and `XMLExtract` to reduce cost of schema inference for large number of files.

# 1.0.3

- Expose numPartitions Optional Parameter for `*Extract`.

# 1.0.2

- add sql validation step to `SQLValidate` configuration parsing and ensure parameters are injected first (including `SQLTransform`) so the statements with parameters can be parsed.

# 1.0.1

- bump to Spark [2.3.1](https://spark.apache.org/releases/spark-release-2-3-1.html).

# 1.0.0

- initial release.