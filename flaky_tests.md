# Flaky tests


One of the most popular reason that tests fail intermittently is because of the assertion of the time. 
One easy way that we found to fix it was to stop time(insert `taps on the forehead` meme).


``` ruby

around(:each) do |example|
  travel_to(Time.zone.parse("2020-03-10")) do
    example.run
  end
end

```
