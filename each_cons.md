`each_cons` method from ruby, which can be run on arrays, hashes and other "enumerable" data structures is quite nice and convenient.

Docs: https://apidock.com/ruby/Enumerable/each_cons

How it works

``` ruby
[1, 2, 3, 4].each_cons(2).to_a
# [[1, 2], [2, 3], [3, 4]]
```

Where I used this

I have a scenario where I have to test if filter for multiple statuses is working fine.

``` ruby
describe TicketFilters do
  TicketStatuses = ["TODO", "ONGOING", "CLOSED"]

  let(:tickets) do
    { "TODO" => create(:ticket, :todo), 
      "ONGOING" => create(:ticket, :ongoing), 
      "CLOSED" => create(:ticket, :closed) }
  end

  TicketStatuses.each_cons(2) do |status1, status2|
    context "when given the status `#{status1} and #{status2}`" do
    it "filters appropriately" do
      result = described_class.new.filter(statuses: [status1, status2])
      expect(result).to match_array(tickets[status1], tickets[status2])
    end
  end
end
```
