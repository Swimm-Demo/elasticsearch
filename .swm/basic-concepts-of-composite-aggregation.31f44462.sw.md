---
title: Basic Concepts of Composite Aggregation
---
# Overview

Composite Aggregation is a specialized type of aggregation that allows for the combination of multiple sources into a single bucket. It is used to efficiently aggregate data across multiple dimensions, enabling complex queries and data analysis.

# <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="94:1:1" line-data="    CompositeAggregator(">`CompositeAggregator`</SwmToken> Class

The <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="94:1:1" line-data="    CompositeAggregator(">`CompositeAggregator`</SwmToken> class is responsible for managing the composite aggregation process, including the collection and sorting of composite buckets.

<SwmSnippet path="/server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" line="94">

---

The constructor of the <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="94:1:1" line-data="    CompositeAggregator(">`CompositeAggregator`</SwmToken> class initializes various components necessary for the aggregation process, such as <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="106:3:3" line-data="        this.sourceNames = Arrays.stream(sourceConfigs).map(CompositeValuesSourceConfig::name).toList();">`sourceNames`</SwmToken>, <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="107:3:3" line-data="        this.reverseMuls = Arrays.stream(sourceConfigs).mapToInt(CompositeValuesSourceConfig::reverseMul).toArray();">`reverseMuls`</SwmToken>, <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="108:3:3" line-data="        this.missingOrders = Arrays.stream(sourceConfigs).map(CompositeValuesSourceConfig::missingOrder).toArray(MissingOrder[]::new);">`missingOrders`</SwmToken>, and <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="109:3:3" line-data="        this.formats = Arrays.stream(sourceConfigs).map(CompositeValuesSourceConfig::format).toList();">`formats`</SwmToken>. It also checks that the provided size does not exceed the <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="111:23:25" line-data="        // check that the provided size is not greater than the search.max_buckets setting">`search.max_buckets`</SwmToken> setting.

```java
    CompositeAggregator(
        String name,
        AggregatorFactories factories,
        AggregationContext aggCtx,
        Aggregator parent,
        Map<String, Object> metadata,
        int size,
        CompositeValuesSourceConfig[] sourceConfigs,
        CompositeKey rawAfterKey
    ) throws IOException {
        super(name, factories, aggCtx, parent, CardinalityUpperBound.MANY, metadata);
        this.size = size;
        this.sourceNames = Arrays.stream(sourceConfigs).map(CompositeValuesSourceConfig::name).toList();
        this.reverseMuls = Arrays.stream(sourceConfigs).mapToInt(CompositeValuesSourceConfig::reverseMul).toArray();
        this.missingOrders = Arrays.stream(sourceConfigs).map(CompositeValuesSourceConfig::missingOrder).toArray(MissingOrder[]::new);
        this.formats = Arrays.stream(sourceConfigs).map(CompositeValuesSourceConfig::format).toList();
        this.sources = new SingleDimensionValuesSource<?>[sourceConfigs.length];
        // check that the provided size is not greater than the search.max_buckets setting
        int bucketLimit = aggCtx.maxBuckets();
        if (size > bucketLimit) {
            logger.warn("Too many buckets (max [{}], count [{}])", bucketLimit, size);
```

---

</SwmSnippet>

# <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="141:9:9" line-data="        this.queue = new CompositeValuesCollectorQueue(aggCtx.bigArrays(), sources, size, aggCtx.searcher().getIndexReader());">`CompositeValuesCollectorQueue`</SwmToken>

The <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="141:9:9" line-data="        this.queue = new CompositeValuesCollectorQueue(aggCtx.bigArrays(), sources, size, aggCtx.searcher().getIndexReader());">`CompositeValuesCollectorQueue`</SwmToken> maintains the priority queue of composite buckets, ensuring efficient collection and retrieval of results.

<SwmSnippet path="/server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" line="141">

---

The <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="141:9:9" line-data="        this.queue = new CompositeValuesCollectorQueue(aggCtx.bigArrays(), sources, size, aggCtx.searcher().getIndexReader());">`CompositeValuesCollectorQueue`</SwmToken> is initialized within the <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="94:1:1" line-data="    CompositeAggregator(">`CompositeAggregator`</SwmToken> class. If a <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/CompositeAggregator.java" pos="142:4:4" line-data="        if (rawAfterKey != null) {">`rawAfterKey`</SwmToken> is provided, it sets the after key for the queue, handling any potential exceptions.

```java
        this.queue = new CompositeValuesCollectorQueue(aggCtx.bigArrays(), sources, size, aggCtx.searcher().getIndexReader());
        if (rawAfterKey != null) {
            try {
                this.queue.setAfterKey(rawAfterKey);
            } catch (IllegalArgumentException ex) {
                throw new ElasticsearchParseException(
                    "Cannot set after key in the composite aggregation [" + name + "] - " + ex.getMessage(),
                    ex
                );
            }
        }
```

---

</SwmSnippet>

# <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="40:1:1" line-data="        CompositeAggregation {">`CompositeAggregation`</SwmToken> Interface

The <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="40:1:1" line-data="        CompositeAggregation {">`CompositeAggregation`</SwmToken> interface defines the structure of the composite aggregation, including methods for retrieving buckets and the last key used in the aggregation.

<SwmSnippet path="/server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" line="52">

---

The <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="52:1:1" line-data="    InternalComposite(">`InternalComposite`</SwmToken> class implements the <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="40:1:1" line-data="        CompositeAggregation {">`CompositeAggregation`</SwmToken> interface. It manages the internal state of the composite aggregation, including <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="55:6:6" line-data="        List&lt;String&gt; sourceNames,">`sourceNames`</SwmToken>, <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="56:6:6" line-data="        List&lt;DocValueFormat&gt; formats,">`formats`</SwmToken>, <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="57:6:6" line-data="        List&lt;InternalBucket&gt; buckets,">`buckets`</SwmToken>, <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="58:3:3" line-data="        CompositeKey afterKey,">`afterKey`</SwmToken>, <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="54:3:3" line-data="        int size,">`size`</SwmToken>, <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="59:5:5" line-data="        int[] reverseMuls,">`reverseMuls`</SwmToken>, <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="60:5:5" line-data="        MissingOrder[] missingOrders,">`missingOrders`</SwmToken>, and <SwmToken path="server/src/main/java/org/elasticsearch/search/aggregations/bucket/composite/InternalComposite.java" pos="61:3:3" line-data="        boolean earlyTerminated,">`earlyTerminated`</SwmToken>.

```java
    InternalComposite(
        String name,
        int size,
        List<String> sourceNames,
        List<DocValueFormat> formats,
        List<InternalBucket> buckets,
        CompositeKey afterKey,
        int[] reverseMuls,
        MissingOrder[] missingOrders,
        boolean earlyTerminated,
        Map<String, Object> metadata
    ) {
        super(name, metadata);
        this.sourceNames = sourceNames;
        this.formats = formats;
        this.buckets = buckets;
        this.afterKey = afterKey;
        this.size = size;
        this.reverseMuls = reverseMuls;
        this.missingOrders = missingOrders;
        this.earlyTerminated = earlyTerminated;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBZWxhc3RpY3NlYXJjaCUzQSUzQVN3aW1tLURlbW8=" repo-name="elasticsearch" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
