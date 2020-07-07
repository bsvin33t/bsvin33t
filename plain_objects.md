Plain objects(non persisted ones), are very powerful.
Here is an anecdote where I and my colleagues found it to be of a lot of help.

We wanted to store file attachments using shrine as "activities". 
This activity would be used to obtain the URL in a later point of time. 
The problem here was the URL would expire in 15 mins. The question was how do we fetch the attached files?

The way I suggested was, we store the metadata that shrine uses in a JSONB column, 
when we want the attachments in the activity, 
then we instantiate an "attachment" object with the shrine metadata that we stored on the activity and generate the URL from it.

Here is the sample code that we used:

``` ruby

class Attachment < ApplicationRecord
  include TicketAttachmentUploader::Attachment.new(:file)
end

class AttachmentActivity < ApplicationRecord
  store :parameters
  store_accessor :parameters, :file_data
end

class CreateAttachment
  # some code to create an actual attachment object and call `create_activity` method

  def create_activity(file_data)
    AttachmentActivity.create!(parameters: { file_data: file_data })
  end
end
```

Once the activity object is persisted, and we want to fetch it in a later point of time, we can just do this:

``` ruby
activity = AttachmentActivity.where(id: id)

attachment_url = Attachment.new(file_data: activity.file_data).download_url

```
