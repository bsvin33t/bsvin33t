### data uri shrine plugin

You get a raw stream of data, maybe as a string, but you want to upload it to S3 using shrine, use data uri shrine plugin, by setting the appropriate content type.


``` ruby
data = "some_base_64_encoded_data_in_string"

file = AttachmentUploader.data_uri(
  "data:#{content_type};base64,#{data}",
  filename: file_name
)
```

If images are to be attached inline, in an email, this is a neat technique too!
