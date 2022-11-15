# Test Cases and Dataset Requirements

In order to have a realistic benchmark we need a dedicated dataset for the different scenarios we want to test, there are three main scenarios:

1. **[CASE]** Validation of the encoding and decoding procedures of OTLP to OTLP Arrow
    - **[DATASET]** - Exhaustivity - Testing the encoding mechanism under every permutation and variation of traces to ensure proper behavior of types translations
        - Verify that all Trace fields are covered
        - Nested object (links, events, etc.)
    - **[DATASET]** - Malformed - This dataset is composed of malformed traces and should test the robustness of the encoding mechanism
        - Missing required field
        - UUID (i.e Trace ID) fields don’t have the right size
        - Field value out of the acceptable values (enum)
        - Different types (number instead of string)
        - Very huge Trace requests
            - Single Trace with many spans
            - Medium side trace with a huge field inside > 10MB (i.e payload)
            - Note: There is already a limitation in the gRPC API to ensure we can't be overloaded with huge messages, though there are some cases where the overall request is under that limit but includes a very big field within it
            - Empty fields
            - Malformed trace request (TBD)
2. **[CASE]** Testing the OTLP Arrow compression ratio for different types of realistic use-cases
    - **[DATASET]** - Super Realistic -  This dataset is composed of traces that can represent a common production topology and can be accepted as the main benchmarking dataset, one that represents a wide variety of traces all together
        - High cardinality field values - Traces with very high variations of field values
            - Note: Some of the limitation of existing tests is the use of dictionaries which have limit on the type of keys used
        - Variation not only in the attribute value but also in the number of attributes

## Delivery

- Generate the traces in a binary format according to the protobuf traces schema
- Already exists - a tool to read the protobuf manages and compare compression rates

## Open Questions

- Timespan
- Hosting (s3)
- Dediacted repo
- Missing features (should we open to public now?
