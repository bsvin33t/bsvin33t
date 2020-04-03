RSpec allows setting metadata in the example runs.

One very nice thing that we can see is using metadata to turn on and off the feature toggles for specific tests.

```ruby
config.around(:each, :toggle) do |example|
  Toggle.enable(example.metadata[:flipper])
  example.run
  Toggle.disable(example.metadata[:flipper])
end
```

by setting the key `:toggle` to a value will allow us to enable and disable the feature when testing. Very nice
