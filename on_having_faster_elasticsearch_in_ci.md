## Faster elasticsearch tests in CI or in Test env

It always feels nice to have fast test. One of the things that slows us down is having elasticsearch turn on and offon every test run.
Instead of doing this, we can have an ES instance running all the time. Neat, innit?

Here is an example of how we do it in our project.

In our `.env.test` file:

``` env
USE_EXISTING_TEST_ES_CLUSTER=true
```
We have this env var. Now where do we use this env var, you ask.

In our `rails_helper.rb` file:

``` ruby
config.before(:suite, elasticsearch: true) do
  if !ENV["USE_EXISTING_TEST_ES_CLUSTER"] &&
      !Elasticsearch::Extensions::Test::Cluster.running?(
        on: ENV["ELASTICSEARCH_PORT"]
      )
    Elasticsearch::Extensions::Test::Cluster.start(
      port: ENV["ELASTICSEARCH_PORT"],
      nodes: ENV["TEST_CLUSTER_NODES"],
      timeout: 120
    )
  end
end

config.after(:suite) do
  if !ENV["USE_EXISTING_TEST_ES_CLUSTER"] &&
      Elasticsearch::Extensions::Test::Cluster.running?(
        on: ENV["ELASTICSEARCH_PORT"]
      )
    Elasticsearch::Extensions::Test::Cluster.stop(
      port: ENV["ELASTICSEARCH_PORT"],
      nodes: ENV["TEST_CLUSTER_NODES"]
    )
  end
end
```

Sometimes Elasticsearch might need some cleanup. I have this handy script that does it:

``` shell
curl -XGET "localhost:9200/_cat/indices?v" | awk "{ print \$3 }" | while read IND ; do curl -XDELETE "localhost:9200/$IND" ; done

```
