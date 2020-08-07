### GraphQL schema validation

There are 2 ways to ensure that the schema is up to date with the applications.

One way, write the schema by hand and generate code from it, another, genrating schema from code.

We use the latter in our org, as we are using [graphql-ruby](https://github.com/rmosolgo/graphql-ruby)

To ensure that our production schema is up to date with our app, we have this checked into our app's build pipeline:


``` ruby

if Rails.env.development? || Rails.env.test?
  require "rspec/support/differ"

  namespace :graphql do
    namespace :schema do
      desc "Validate the dumped schema"
      task validate: :environment do
        actual_schema = GraphQL::Schema::Printer.print_schema(SpAdminSchema, context: { rake: true })
        dumped_schema = File.read(Rails.root.join("app", "graphql", "schema.graphql"))

        if actual_schema != dumped_schema
          print RSpec::Support::Differ.new.diff(dumped_schema, actual_schema)

          abort "GraphQL Schema is out of date. Please run rake graphql:schema:idl"
        end
      end
    end
  end
end

```
