I am given a private file URL uploaded to S3 via presigned URL. I have programmatic access to S3.
How do I download it.

Here it is: 

```ruby
  def s3_url(media_url, storage:)
    key = s3_key(media_url, storage: storage)
    Shrine.storages[storage].url(key)
  end

  def s3_key(media_url, storage:)
    key = media_url
      .delete_prefix(Shrine.storages[storage].bucket.url + directory(storage))

    CGI.unescape(key)
  end

  def directory(storage)
    # Special behavior for cache storage because of the shrine configuration.
    # See configuration in persistence/config/initializers/shrine.rb
    return "/cache/" if storage == :cache

    "/"
  end
```

Please feel free to raise an issue if you felt this post needs more information.

Cheers

Vineeth

