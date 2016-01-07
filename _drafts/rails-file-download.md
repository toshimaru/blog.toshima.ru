
```rb
class PdfController < ApplicationController
  def download
    filepath = Rails.root.join('resource', 'download.pdf')
    stat = File::stat(filepath)
    send_file(filepath, :filename => 'download.pdf', :length => stat.size)
  end
end
```
