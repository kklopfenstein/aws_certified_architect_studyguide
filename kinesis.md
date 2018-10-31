Kinesis
----------

* Kinesis 101
  * What is streaming data
    * Streaming Data is data that is generated continuously by thousands of data sources, which typically send in the data records simultaneously, and in small sizes ( order of kilobytes).
      * Purchases from online stores ( think amazon.com)
      * Stock Prices
      * Game data (as the gamer plays)
      * Social network data
      * Geospatial data (think uber.com)
      * iOT sensor data
  * Kinesis is a platform on AWS to send your streaming data too. Kinesis makes it easy to load and analyze streaming data, and also providing the ability for you to build your own custom applications for your business needs.
  * Kinesis Streams, Kinesis Firehose, Kinesis Analytics
  * Kinesis Streams
    * Stores data for 24 hours - can be up to 7 days
    * Consists of shards
      * 5 transactions per second for reads, up to a maximum total data read rate of 2 MB per second and up to 1,000 records per second for writes, up to a maximum total data write rate of 1 MB per second (including partition keys).
      * The data capacity of your sream i sa function of the number of shards that you specify for the stream. The total capacity of the stream is the sum of the capacities of its shards.
  * Kinesis Firehose
    * No shards/streams
    * As soon as data comes in, it's analyzed or sent to S3/other locations (e.g. redshift
  * Kinesis Analytics
    * Allows you to run SQL queries in Firehose, Streams.
    * Use query to store in S3, Redshift, or Elasticsearch Cluster
