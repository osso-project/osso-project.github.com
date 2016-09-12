# Osso - A modern standard for event-oriented data

Our world is made up of _events_. We as developers commonly work with log
messages, metric samples, HTTP requests, ad impressions and clicks, user
behavior and actions (e.g. abandoned shopping cart, like, favorite), security
events, application and system diagnostics, player actions in online games, and
so on. The lines between different types of events are blurry at best, and, in
most cases, completely arbitrary. Login events can be thought of as security
events, user actions, HTTPS events from a web application, or system diagnostic
events. A consumer-focused application cares about the impact of ads or app
crashes on user experience and usage. All services providers understand
operational issues impact customer engagement and churn. Still, our industry has
historically thought of, and represented, this data in very different ways.

The dividing line between business transactional data and operational data no
longer exists. Or, at least it shouldn't.

Further, the way we build modern systems is changing and, in a lot of ways,
trending toward thinking about the world in terms of events. We're increasingly
embracing stream processing as the dominant paradigm for data processing.
Distributed systems, which are commonplace in today's architectures, use
messages (or events) to communicate between components. External SaaS and cloud
systems are, in many ways, just another distributed component of a larger system
requiring integration by way of API calls, themselves just a pair of
request/response events. The complexity of these modern systems requires a new
level of observability; yet another set of events. Some frameworks and models
for developing complex real-time systems such as [Erlang/OTP][erlang] and
[Akka][akka] have made excellent arguments about _why_ systems should be event-
or message-driven, but have stopped short of defining an event, or how it works
across systems.

[erlang]: https://www.erlang.org/
[akka]: http://akka.io/

Today, each one of these domains uses a different representation, set of
semantics, and nomenclature for events. In turn, developers dedicate significant
time building integration and compatibility code between systems. This leads to
inefficient code, endless complexity, a myriad of bugs, and worst of all,
[bikeshedding][law-of-triviality].

[law-of-triviality]: https://en.wikipedia.org/wiki/Law_of_triviality

Understanding how these events relate to one another is a prerequisite to
understanding the systems or domains they represent. Is an online store session
termination immediately preceded by an application crash or HTTP 500 response?
Has the number of HTTP 500 responses increased recently? What events preceded
the increase in errors? Has a new version of the store checkout code been
deployed recently? Who authorized the push to production? Are customer
complaints about the checkout process increasing? Exactly which users have been
negatively affected by the change? What percentage of them contacted support?
What was the total monetary value of the failed transactions for the affected
users that didn't contact support? In order to correlate these events, we need
to have a common understanding - in both format and semantics - of the type of
an event, the time at which it occurred, the source where it originated, and a
way to represent event type-specific information. This allows us to build
_context_ by having a singular model for representing what is happening across
systems and services, from devices and infrastructure to users and transactions,
in code we write and third-party code that we adopt or buy.

## A Modern Standard

We need a standard for event-oriented data.

Our event data must be _open_ to be useful. A single entity or vendor must not
be able to control how, when, or where we use our data. We must be free to
choose the languages, frameworks, tools, and systems that are right for us.
Similarly, commercial vendors should be able to add support for any such
standard without fear of onerous licenses or commitments. A community of users
must be able to collaborate and share implementations and supporting
functionality around any standard.

A standard must be _easy and intuitive_ to succeed. In fact, to the extent
possible, it should be a representation of what developers are already doing,
capturing the best elements of what has been proven in production systems. Those
new to the field or the space should be able to intuitively do the "right
thing," rather than steeping themselves in heaps of documentation. A standard
should be minimally invasive to existing code and thinking.

Any standard for data must be _efficient_. Event data comes from all kinds of
devices, from low power mobile phones all the way to servers and mainframes. It
must be efficient to represent in memory, on the wire, and on disk.

Finally, a standard must be _complementary_ with existing technology. Where
possible, it should not reinvent reasonably well-solved problems, instead,
opting to build on top of existing standards, _de facto_ or formal.

## Meet Osso

Osso is a modern standard for event-oriented data. Osso consists of a schema, a
set of well-defined semantics, and a production-ready reference implementation
for representing events in a wide variety of systems and situations.

Osso is...

* **Open**

  Osso is open source, [hosted on Github][osso-github], and available under the
  [Apache License 2.0][osso-licenses]

  Osso's event schema is defined as an [Apache Avro][apache-avro] schema, making
  Osso events compatible with any system that understands Avro schemas or
  serialized data.

  [Osso's schema and semantics are defined][osso-readme] separately for cases
  where highly-specialized serialization is more important than the ease of use
  or compatibility afforded by Avro. This also makes Osso compatibility layers
  easy to implement.

[osso-github]: https://github.com/osso-project/osso
[osso-license]: https://github.com/osso-project/osso/blob/master/LICENSE
[apache-avro]: http://avro.apache.org/
[osso-readme]: https://github.com/osso-project/osso/blob/master/README.md

* **Easy and Intuitive**

  Osso events can be represented in memory as simple objects (e.g. POJOs) or
  records.

  Events are semi-structured, with common fields representing elements every
  event has, and key/value attributes for event type-specific fields.

  Events have a simple but complete representation of time. Time is always a
  millisecond precision epoch timestamp in UTC.

  Events have a pure method for producing a unique event ID making
  de-duplication and other common tasks easy.

  Event types are a highly flexible way of communicating event metadata to
  event consumers or recipients.

  A single semi-structured schema is used to represent all event types,
  eliminating the need to do awkward type negotiation for events. Event types
  can be used to detect specific types of events for customized processing.

  Event types are easily extended without requiring code changes or
  recompilation unless custom processing is required, making building generic
  event processing systems straight forward.

* **Efficient**

  Osso events have a minimal number of fields making their serialized
  representation as small as possible. Apache Avro is well known for having a
  reasonable balance of CPU and size efficiency. Osso uses pre-shared Avro
  schemas.

* **Complementary**

  Osso uses Apache Avro to define its schema as well as its serialization
  format rather than defining a new format. Avro was selected for its balance
  between CPU and size efficiency, cross language compatibility, and third party
  system support.

  The event schema and semantics are an amalgam of generally accepted "best
  practices" for representing this kind of data.

If you build or integrate event-oriented systems, join us in building a
modern standard at the [Osso project][osso-github].

Show your supported for Osso by adding yourself to the [list of product and
projects powered by Osso][osso-poweredby].

[osso-poweredby]: https://github.com/osso-project/osso-project.github.io/blob/master/powered-by.md
