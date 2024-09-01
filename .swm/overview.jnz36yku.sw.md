---
title: Overview
---
The repo `elasticsearch` is a distributed search and analytics engine that is optimized for speed and relevance on production-scale workloads. It serves as a scalable data store and vector database, enabling use cases such as full-text search, logs, metrics, application performance monitoring (APM), security logs, vector search, and integration with generative AI applications.

## Main Components

### Server Core

Server Core refers to the essential components and functionalities that form the backbone of the server-side operations. It includes the main classes, methods, and resources necessary for the server to function, such as handling requests, managing configurations, and ensuring communication between different parts of the system. Server Core is crucial for maintaining the stability, performance, and scalability of the server.

- <SwmLink doc-title="Gateway in server core">[Gateway in server core](.swm/gateway-in-server-core.blvjp7nr.sw.md)</SwmLink>
- <SwmLink doc-title="Basic concepts of nodeclient">[Basic concepts of nodeclient](.swm/basic-concepts-of-nodeclient.h6t125d2.sw.md)</SwmLink>
- <SwmLink doc-title="Overview of telemetry in server core">[Overview of telemetry in server core](.swm/overview-of-telemetry-in-server-core.bljyismy.sw.md)</SwmLink>
- <SwmLink doc-title="Basic concepts of task management">[Basic concepts of task management](.swm/basic-concepts-of-task-management.95j0707p.sw.md)</SwmLink>
- **Rest**
  - <SwmLink doc-title="Overview of rest api functionality">[Overview of rest api functionality](.swm/overview-of-rest-api-functionality.ftis51d0.sw.md)</SwmLink>
  - <SwmLink doc-title="Basic concepts of cat apis">[Basic concepts of cat apis](.swm/basic-concepts-of-cat-apis.kundj8uw.sw.md)</SwmLink>
  - **Admin**
    - <SwmLink doc-title="Exploring indices in admin">[Exploring indices in admin](.swm/exploring-indices-in-admin.8b2qxydr.sw.md)</SwmLink>
    - <SwmLink doc-title="Exploring cluster management">[Exploring cluster management](.swm/exploring-cluster-management.sygz10sb.sw.md)</SwmLink>
- **Search**
  - <SwmLink doc-title="Overview of ranking in search">[Overview of ranking in search](.swm/overview-of-ranking-in-search.c02z962j.sw.md)</SwmLink>
  - <SwmLink doc-title="Getting started with fetch phase">[Getting started with fetch phase](.swm/getting-started-with-fetch-phase.m4m478w6.sw.md)</SwmLink>
  - <SwmLink doc-title="Basic concepts of search lookup">[Basic concepts of search lookup](.swm/basic-concepts-of-search-lookup.kw70vtoq.sw.md)</SwmLink>
  - <SwmLink doc-title="Introduction to internal search components">[Introduction to internal search components](.swm/introduction-to-internal-search-components.etq3gd4u.sw.md)</SwmLink>
  - <SwmLink doc-title="Basic concepts of runtime in search">[Basic concepts of runtime in search](.swm/basic-concepts-of-runtime-in-search.wmil06c8.sw.md)</SwmLink>
  - **Aggregations**
    - <SwmLink doc-title="Getting started with aggregation support">[Getting started with aggregation support](.swm/getting-started-with-aggregation-support.woxvh41w.sw.md)</SwmLink>
    - <SwmLink doc-title="Overview of pipeline aggregations">[Overview of pipeline aggregations](.swm/overview-of-pipeline-aggregations.q25i0g0x.sw.md)</SwmLink>
    - **Bucket**
      - <SwmLink doc-title="Introduction to histogram aggregation">[Introduction to histogram aggregation](.swm/introduction-to-histogram-aggregation.i9q8zkez.sw.md)</SwmLink>
      - <SwmLink doc-title="Exploring range aggregation">[Exploring range aggregation](.swm/exploring-range-aggregation.mysbux4a.sw.md)</SwmLink>
      - <SwmLink doc-title="Sampler aggregation in elasticsearch">[Sampler aggregation in elasticsearch](.swm/sampler-aggregation-in-elasticsearch.lfxjqat1.sw.md)</SwmLink>
      - <SwmLink doc-title="Basic concepts of composite aggregation">[Basic concepts of composite aggregation](.swm/basic-concepts-of-composite-aggregation.31f44462.sw.md)</SwmLink>
      - <SwmLink doc-title="Basic concepts of geogrid aggregation">[Basic concepts of geogrid aggregation](.swm/basic-concepts-of-geogrid-aggregation.7lrgmbbv.sw.md)</SwmLink>
      - <SwmLink doc-title="Introduction to terms in bucket aggregations">[Introduction to terms in bucket aggregations](.swm/introduction-to-terms-in-bucket-aggregations.ph0qxlux.sw.md)</SwmLink>
    - **Metrics**
      - <SwmLink doc-title="Introduction to metrics in aggregations">[Introduction to metrics in aggregations](.swm/introduction-to-metrics-in-aggregations.s6ypthxc.sw.md)</SwmLink>
      - <SwmLink doc-title="Getting started with cardinality aggregator in metrics">[Getting started with cardinality aggregator in metrics](.swm/getting-started-with-cardinality-aggregator-in-metrics.hyvqqocv.sw.md)</SwmLink>
      - <SwmLink doc-title="Getting started with hyperloglog algorithm in metrics">[Getting started with hyperloglog algorithm in metrics](.swm/getting-started-with-hyperloglog-algorithm-in-metrics.1colc7r7.sw.md)</SwmLink>
      - <SwmLink doc-title="Overview of immutable empty hdr histogram">[Overview of immutable empty hdr histogram](.swm/overview-of-immutable-empty-hdr-histogram.0fzwcvib.sw.md)</SwmLink>
      - <SwmLink doc-title="Percentiles configuration in metrics">[Percentiles configuration in metrics](.swm/percentiles-configuration-in-metrics.rb8b4jed.sw.md)</SwmLink>
      - <SwmLink doc-title="Getting started with global ordinal aggregator in metrics">[Getting started with global ordinal aggregator in metrics](.swm/getting-started-with-global-ordinal-aggregator-in-metrics.g2dkg9wt.sw.md)</SwmLink>
      - <SwmLink doc-title="Extended stats in metrics">[Extended stats in metrics](.swm/extended-stats-in-metrics.xfhmxj90.sw.md)</SwmLink>
  - **Profile**
    - <SwmLink doc-title="Getting started with search profiling">[Getting started with search profiling](.swm/getting-started-with-search-profiling.24k4a9wo.sw.md)</SwmLink>
    - <SwmLink doc-title="Overview of query profiling">[Overview of query profiling](.swm/overview-of-query-profiling.clite464.sw.md)</SwmLink>
  - **Subphase**
    - <SwmLink doc-title="Overview of fetch subphase">[Overview of fetch subphase](.swm/overview-of-fetch-subphase.hvkkkqkm.sw.md)</SwmLink>
    - <SwmLink doc-title="Exploring highlight functionality">[Exploring highlight functionality](.swm/exploring-highlight-functionality.qull1h2h.sw.md)</SwmLink>
  - **Suggest**
    - <SwmLink doc-title="Understanding completion in suggest">[Understanding completion in suggest](.swm/understanding-completion-in-suggest.rq46bwml.sw.md)</SwmLink>
    - <SwmLink doc-title="Introduction to phrase suggestion">[Introduction to phrase suggestion](.swm/introduction-to-phrase-suggestion.b5c90jei.sw.md)</SwmLink>
- **Classes**
  - <SwmLink doc-title="The writeable class">[The writeable class](.swm/the-writeable-class.48i8e.sw.md)</SwmLink>
  - <SwmLink doc-title="The actionresponse class">[The actionresponse class](.swm/the-actionresponse-class.z1bno.sw.md)</SwmLink>
  - <SwmLink doc-title="The handledtransportaction class">[The handledtransportaction class](.swm/the-handledtransportaction-class.4f312.sw.md)</SwmLink>

## Classes

- <SwmLink doc-title="The toxcontentobject class">[The toxcontentobject class](.swm/the-toxcontentobject-class.anlhi.sw.md)</SwmLink>
- <SwmLink doc-title="The releasable class">[The releasable class](.swm/the-releasable-class.c4kum.sw.md)</SwmLink>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBZWxhc3RpY3NlYXJjaCUzQSUzQVN3aW1tLURlbW8=" repo-name="elasticsearch" doc-type="other"><sup>Powered by [Swimm](/)</sup></SwmMeta>
