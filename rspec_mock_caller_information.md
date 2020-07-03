# RSpec mock's caller information.

Yesterday, I had a very hard time trying to figure out from where my object's method was receiveing a 2nd call, because of which my mocked expectation was failing.

I searched for the term `expected: 1 time with any arguments received: 2 times with any arguments + mock + rspec`

Lo and behold, I got this in the 3rd result: https://github.com/rspec/rspec-mocks/issues/939

This piece of code, clearly showed me from where the calls were occouring. Thanks to the community, I was able get information about a new feature on RSpec.

```ruby
allow(MyModel).to receive(:find).and_wrap_original do |original, *args|
  puts "Category.find is begin called from:"
  puts caller.join("\n")
  puts

  original.call(*args)
end

MyModel.some_method
```
