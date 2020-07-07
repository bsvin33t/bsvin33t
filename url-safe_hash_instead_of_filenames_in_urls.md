### URL safe hash instead of filenames in URLs.
### Summary

Turns out having filenames in URLs is kinda annoying because people can put anything in there. We have been en- and decoding the download URLs to get around that but didn't really trust that this fixes all the possible issues. So now we're not using the filename anymore. Instead we're generating a url-safe base64 hash and use that in the URL.

When previously the URL looked like this:

```
http://localhost:4000/public/bucket/public/categories/original/example.jpg
```

It now looks like this:

```
http://localhost:4000/public/bucket/public/eyJpZCI6ImNhdGVnb3JpZXMvb3JpZ2luYWwvcmF1bWdlc3RhbHR1bmcuanBnIn0
```

This could also be extended to encode more data in the future if we find a need for that.

``` ruby
class UrlsafeSerializer
  class << self
    def serialize(data)
      json = JSON.generate(data)

      Base64.urlsafe_encode64(json, padding: false)
    end

    def deserialize(string)
      json = Base64.urlsafe_decode64(string)

      if json.match?(/[^[:ascii:]]/)
        raise ArgumentError, "Only accepts base64 encoded strings."
      end

      JSON.parse(json, symbolize_names: true)
    end
  end
end


```
