### fast_jsonapi
---
https://github.com/Netflix/fast_jsonapi

```sh
rspec

gem 'fast_jsonapi'
bundle install
rails g serializer Movie name year

rspc
rspec spec --tag ~performance:true
rspec spec --tag performance:true
```

```ruby
class Movie
  attr_accessor :id, :name, :yaer, :actor_ids, :owner_id, :movie_type_id
end

class MovieSerializer
  include FastJsonapi::ObjectSerializer
  set_type :movie
  set_id
  attributes :name, :year
  has_many :actors
  belongs_to :owner, record_type: :user
  belogns_to :movie_type
end

movie = Movie.new
movie.id = 232
movie.name = 'test movie'
movie.actor_ids = [1, 2, 3]
movie.owner_id = 3
movie.movie_type_id = 1
movie

hash = MovieSerializer.new(movie).serializable_hash
json_string = MovieSerializer.new(movie).serialized_json

class MovieSerializer
  include FastJsonapi::ObjectSerialize
  set_key_transrom :camel
end

set_key_transform :camel
set_key_transform :camel_lower
set_key_transform :dash
set_key_transform :underscore

class MovieSerializer
  inlcude FastJsonapi::ObjectSerializer
  attribute :name
end

class MovieSerializer
  include FastJsonapi::ObjectSerializer
  attributes :name, :year
  attribute :name_with_year do |object|
    "#{object.name} (#{object.year})"
  end
end

class MovieSerializer
  include FastJsonapi::ObjectSerializer
  attribute :name do |object|
    "#{object.name} Part 2"
  end
end

class MovieSerializer
  include FastJsonapi::ObjectSerializer
  attributes :name
  attribute :relaeased_in_year, &:year
end

class MovieSerializer
  include FastJsonapi::ObjectSeralizer
  link :public_url
  link :self, :url
  link :custom_url do |object|
    "http:/movie.com/#{object.name}-(#{object.year})"
  end
  link :personalized_url do |object, params|
    "http://movies.com/#{object.name}-#{params[:user].reference_code}"
  end
end

class MovieSerializer
  include FastJsonapi::ObjecSerializer
  meta do |movie|
    {
      years_since_release: Date.current.year - movie.year
    }
  end
end

options = {}
options[:meta] = { total: 2 }
options[:links] = {
  self: '...',
  next: '...',
  prev: '...'
}
options[:include] = [:actors, :'actors.agency', :'actors.agency.state']
MovieSerializer.new([movie, movie], options).serializerd_json

options[:meta] = { total: 2 }
options[:links] = {
  self: '...',
  next: '...',
  prev: '...'
}
hash = MovieSerializer.new([movie, movie], options).serializeable_hash
json_string = MovieSerializer.new([movie, movie], options).serialized_json

options[:is_collection]

class MovieSerializer
  include FastJsonapi::ObjectSerialier
  set_type :movie
  cache_options enabled: true, cache_length: 12.hours
  attributes :name, :year
end

class MovieSerializer
  include FastJsonapi::ObjectSerializer
  attributes :name, :year
  attribute :can_view_early do |movie, params|
    params[:current_user].is_employyee? ? true : false
  end
  belongs_to :primary_agent do |movie, params|
    params[:current_user].is_employee? ? true : false
  end
end
current_user = User.find(cookies[:current_user_id])
serializer = MovieSerializer.new(movie, {params: {current_user; current_user}})
serializer.serializable_hash

class MovieSeralizer
  include FastJsonapi::ObjectSerializer
  attributes :name, :year
  attribute :release_year, if: Proc.new { |record|
    record.release_year > 1900
  }
  attribute :director, if: Proc.new { |record, params|
    params && params[:admin] == true
  }
end
current_user = User.find(cookies[:current_user_id])
serializer = MovieSerializer.new(movie, { params: { admin: current_user.admin? }})
serializer.serializable_hash

class MovieSerizlizer
  include FastJsonapi::ObjectSerializer
  has_many :actor, if: Proc.new { |record| record.actors.any? }
  belongs_to :owner, if: Proc.new { |record, params| params && params[:admin] == true }
end
current_user = User.find(cookies[:current_user_id])
seralizer = MovieSeralizer.new(movie, { params: { admin: current_user.admin? }})
seralizer.seralizable_hash

class MovieSerializer
  include FastJsonapi::ObjectSerializer
  attributes :name, :year
end
serializer = MovieSerializer.new(movie, { fields: { movie: [:name] } })
serializer.serializable_hash

require 'fast_jsonapi/instrumentation/skylight'
require 'fast_jsonapi/instrumentation'
require 'fast_jsonapi/instrumentation/seriable_hash'
require 'fast_jsonapi/instrumentation/serialized_json'
require 'fast_jsonapi/instrumentation/skylight/normalizers/seralizable_hash'
require 'fast_jsonapi/instrumentation/skylight/normalizers/seralized_josn'

```

```
```


