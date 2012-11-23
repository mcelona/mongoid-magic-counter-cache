Mongoid Magic Counter Cache [![Build Status](https://secure.travis-ci.org/mcelona/mongoid-magic-counter-cache.png?branch=master)](http://travis-ci.org/jah2488/mongoid-magic-counter-cache)
=======

## DESCRIPTION

Mongoid Counter Cache is a simple mongoid extension to add basic counter cache functionality to Embedded and Referenced Mongoid Documents.
### RDOC
[http://rdoc.info/github/mcelona/mongoid-magic-counter-cache/master/frames](http://rdoc.info/github/mcelona/mongoid-magic-counter-cache/master/frames)

## INSTALLATION

### RubyGems
````sh
$ [sudo] gem install mongoid_magic_counter_cache
````
### GemFile
````rb
gem 'mongoid_magic_counter_cache'
````
## USAGE

First add a field to the document where you will be accessing the counter cache from.

````rb
class Library
  include Mongoid::Document

  field :name
  field :city
  field :book_count
  has_many :books

end
````
Then in the referrenced/Embedded document. Include `Mongoid::MagicCounterCache`

````rb
class Book
  include Mongoid::Document
  include Mongoid::MagicCounterCache

  field :first
  field :last

  belongs_to    :library
  counter_cache :library
end
````

````rb
$ @library.book_count
#=> 990
````
### Alternative Syntax

If you do not wish to use the `model_count` naming convention, you can override the defaults by specifying the `:field` parameter.

````rb
counter_cache :library, :field => "total_amount_of_books"
````

## TODO

  1. Add additional options parameters
  2. Simplify syntax (I.E. including MagicCounterCache will add counts for all `belongs_to` associations on a document



## CONTRIBUTE

If you'd like to contribute, feel free to fork and merge until your heart is content
