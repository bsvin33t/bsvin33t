Managing alphabetical sorting is quite nice when it comes to yml files. Here is something that can be used to manage the sorting.


```ruby

require "rails_helper"

RSpec.describe "Locale files" do
  def sorted_hash?(object, path)
    object.each_cons(2).reduce(true) do |sorted, (a, b)|
      next sorted if a[0] < b[0]

      if a[0] == b[0]
        puts "Warning: Duplicate key #{path}.#{a[0]}"
        next sorted
      end

      puts "Error: Key #{path}.#{a[0]} should be after #{path}.#{b[0]}"
      false
    end
  end

  def deeply_sorted_hash?(object, path: nil)
    return true unless object.is_a?(Hash)

    sorted = sorted_hash?(object, path)

    object.each do |key, value|
      sorted = deeply_sorted_hash?(value, path: [path, key].compact.join(".")) && sorted
    end

    sorted
  end

  it "are alphabetically ordered" do
    aggregate_failures do
      (
        Dir.glob(Rails.root.join("config", "locales", "**", "*.yml"))
      ).each do |file|
        contents = YAML.safe_load(File.read(file), [Symbol])

        ordered = deeply_sorted_hash?(contents)

        puts "\t in file #{file}" unless ordered
        expect(ordered).to be(true), "expected file #{file} to be alphabetically ordered."
      end
    end
  end
end
```
