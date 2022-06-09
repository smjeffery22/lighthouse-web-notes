# RUBY ACTIVE RECORD

`.where` returns a new relation, which is the result of filtering the current relation according to the conditions in the arguments.
  - return an instance of `ActiveRecord::Relation`

`.find_each` retrieves records in batches and then yields each one to the block
  - works in model classes and relations