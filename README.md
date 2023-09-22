# cv_template
cv template

# File 
> 1.html : Html code

> out.pdf : Sample export pdf of generate cv by PDFkit

> 1.py : sample python code

## Note
Thus tailwind css cdn link will not work in pdf kit, because PDFKit doesn't load external resources like web browsers do, So we can inject cdn link via 

```py
import pdfkit
import requests

# Define the URL of the CDN-hosted Tailwind CSS
tailwind_cdn_url = 'https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css'

# Fetch the Tailwind CSS from the CDN
tailwind_css = requests.get(tailwind_cdn_url).text

# Your PDF generation options
options = {
    'page-size': 'Letter',
    'margin-top': '0.75in',
    'margin-right': '0.75in',
    'margin-bottom': '0.75in',
    'margin-left': '0.75in',
    'encoding': "UTF-8",
    'custom-header': [
        ('Accept-Encoding', 'gzip')
    ],
    
    'no-outline': None
}

# Fetch your HTML content
html_url = 'http://127.0.0.1:5500/1.html'
html_content = requests.get(html_url).text

# Modify the HTML content to include the fetched Tailwind CSS
modified_html = html_content.replace('</head>', f'<style>{tailwind_css}</style></head>')

# Save the modified HTML content to a temporary file
with open('temp.html', 'w', encoding='utf-8') as temp_file:
    temp_file.write(modified_html)

# Generate the PDF using PDFKit
pdfkit.from_file('temp.html', 'out.pdf', options=options)

# Clean up the temporary HTML file
import os
os.remove('temp.html')
```

