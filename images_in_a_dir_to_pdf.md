I was tasked by a friend to send him all the letters that he received at his postbox.
In the sprit of automating my work slightly, I wrote a script to convert the list of images that I got out of my scanner into a single PDF.

This ruby script takes all the images in the current directory and stitches it into a nice little pdf.
The dependency is the [prawn library](https://github.com/prawnpdf/prawn).

```ruby
require 'prawn'

# Output PDF file name
output_pdf = 'output.pdf'

# Get a list of all image files in the current directory
image_files = Dir.glob("*.jpg") + Dir.glob("*.jpeg") + Dir.glob("*.png")

# Check if there are any image files in the directory
if image_files.empty?
  puts "No image files found in the current directory."
  exit(1)
end

# Initialize a Prawn::Document
pdf = Prawn::Document.new

# Iterate through each image file and add it to the PDF
image_files.each do |image_file|
  begin
    pdf.image image_file, fit: [pdf.bounds.width, pdf.bounds.height]
    pdf.start_new_page unless image_file == image_files.last
  rescue StandardError => e
    puts "Error processing #{image_file}: #{e.message}"
  end
end

# Save the PDF
pdf.render_file(output_pdf)
puts "PDF file '#{output_pdf}' created successfully."

```
