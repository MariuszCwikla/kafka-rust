# Kafka Rust Client

[![Build Status](https://travis-ci.org/spicavigo/kafka-rust.svg?branch=master)](https://travis-ci.org/spicavigo/kafka-rust) [![](http://meritbadge.herokuapp.com/kafka)](https://crates.io/crates/kafka)

## Project Status

This project is starting to be maintained by John Ward, the current status is that I am bringing the project up to date with the latest dependencies, removing deprecated Rust code and adjusting the tests.

## New Home

Welcome to kafka-rust's new home: https://github.com/kafka-rust

## Documentation

- This library is primarily documented through examples in its [APIdocumentation](https://docs.rs/kafka/).
- Documentation about Kafka itself can be found at [its projecthome page](http://kafka.apache.org/).

## Sponsors

Thank you to our sponsors, this helps me to spend more time on this project and also helps with infrastructure

<table>
<tr>
<td>
  <img width="1000" height="0">
    <a href="https://upstash.com/?utm_source=kafka-rust" >
  <img src="https://raw.githubusercontent.com/upstash/sponsorship/master/kafka.png" alt="Upstash" width="260" align="right">
  </a>

<h3>Upstash: Serverless Kafka</h3>

<ul>
    <li>True Serverless Kafka with per-request-pricing</li>
    <li>Managed Apache Kafka, works with all Kafka clients</li>
    <li>Built-in REST API designed for serverless and edge functions</li>
  </ul>

[Start for free in 30 seconds!](https://upstash.com/?utm_source=kafka-rust)

</td>
</tr>
</table>

## Installation

This crate works with Cargo and is on
[crates.io](https://crates.io/crates/kafka). The API is currently
under heavy movement although we do follow semantic versioning (but
expect the version number to grow quickly).

```toml
[dependencies]
kafka = "0.9"
```

To build kafka-rust the usual `cargo build` should suffice. The crate
supports various features which can be turned off at compile time.
See kafka-rust's `Cargo.toml` and [cargo'sdocumentation](http://doc.crates.io/manifest.html#the-features-section).

## Supported Kafka version

`kafka-rust` is tested for compatibility with Kafka 0.8.2 and newer. However,
not all features from Kafka 0.9 and newer are supported yet.

## Examples

As mentioned, the [cargo generateddocumentation](https://docs.rs/kafka/) contains some examples.
Further, standalone, compilable example programs are provided in the
[examples directory of therepository](https://github.com/spicavigo/kafka-rust/tree/master/examples).

## Consumer

This is a higher-level consumer API for Kafka and is provided by the
module `kafka::consumer`. It provides convenient offset management
support on behalf of a specified group. This is the API a client
application of this library wants to use for receiving messages from
Kafka.

## Producer

This is a higher-level producer API for Kafka and is provided by the
module `kafka::producer`. It provides convenient automatic partition
assignment capabilities through partitioners. This is the API a
client application of this library wants to use for sending messages
to Kafka.

## KafkaClient

`KafkaClient` in the `kafka::client` module is the central point of
this API. However, this is a mid-level abstraction for Kafka rather
suitable for building higher-level APIs. Applications typically want
to use the already mentioned `Consumer` and `Producer`.
Nevertheless, the main features or `KafkaClient` are:

- Loading metadata
- Fetching topic offsets
- Sending messages
- Fetching messages
- Committing a consumer group's offsets
- Fetching a consumer group's offsets

## Bugs / Features / Contributing

There's still a lot of room for improvement on `kafka-rust`.
Not everything works right at the moment, and testing coverage could be better.
**Use it in production at your own risk.** Have a look at the
[issue tracker](https://github.com/spicavigo/kafka-rust/issues) and feel free
to contribute by reporting new problems or contributing to existing
ones. Any constructive feedback is warmly welcome!

As usually with open source, don't hesitate to fork the repo and
submit a pull request if you see something to be changed. We'll be
happy to see `kafka-rust` improving over time.

### Integration tests

When working locally, the integration tests require that you must have
Docker (1.10.0+) and docker-compose (1.6.0+) installed and run the tests via the
included `run-all-tests` script in the `tests` directory. See the `run-all-tests`
script itself for details on its usage.

## Creating a topic

Note unless otherwise explicitly stated in the documentation, this
library will ignore requests to topics which it doesn't know about.
In particular it will not try to retrieve messages from
non-existing/unknown topics. (This behavior is very likely to change
in future version of this library.)

Given a local kafka server installation you can create topics with the
following command (where `kafka-topics.sh` is part of the Kafka
distribution):

```
kafka-topics.sh --topic my-topic --create --zookeeper localhost:2181 --partitions 1 --replication-factor 1
```

See also [Kafka's quickstart guide](https://kafka.apache.org/documentation.html#quickstart)
for more information.

## Alternative/Related projects

- [rust-rdkafka](https://github.com/fede1024/rust-rdkafka) is an emerging alternative Kafka client library for Rust based on
  `librdkafka`. rust-rdkafka provides a safe Rust interface to librdkafka.
