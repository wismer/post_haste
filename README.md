# PostHaste

A Ruby library that wraps the JSON endpoints provided for Washington Post articles and blog posts. Potentially suitable for building custom feeds of Washington Post content, in the event that you don't want to actually visit washingtonpost.com. It handles articles and blog posts from the Post's CMS (along with the most recent 15 comments), as well as The Post's WordPress-powered blogs.

Tested under Ruby 1.9.3, 2.0.0 and 2.1.0.

## Installation

Add this line to your application's Gemfile:

    gem 'post_haste'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install post_haste

## Usage

Post Haste currently can accept a URL of a Washington Post article or blog post, and converts that URL into a Ruby object with a number of methods that describe it, including its title, byline, published and updated datetimes, and more:

```ruby
  require 'post_haste'
  include PostHaste

  url = "http://www.washingtonpost.com/blogs/the-fix/post/republicans-on-the-2012-gop-field-blah/2012/03/15/gIQAT7CSFS_blog.html"

  @article = Article.create_from_url(url, 10) # 10 represents number of comments to grab, default is 25.

  @article.title

  => "Republicans on the 2012 GOP field: Blah."

  @article.display_datetime.to_s

  => "2012-03-16T06:30:00-04:00"
  
  @article.comments.first.author

  => "iseasygoing"
  
  @article.comments.first.permalink(@article)
  
  => "http://www.washingtonpost.com/blogs/the-fix/post/republicans-on-the-2012-gop-field-blah/2012/03/15/gIQAT7CSFS_comment.html?commentID=washingtonpost.com/ECHO/item/1332046095-915-174"
```
  
See the full list of `Article` instance methods in article.rb.

## In the Wild

  See an example application at http://postcomments.herokuapp.com/

### Tests

To run the test suite, do:

  rake test

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
