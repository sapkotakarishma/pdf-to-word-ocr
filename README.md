# pdf-to-word-ocr

git commit -m "Initial commit: PDF to Word OCR project"

!pip install pytesseract python-docx pdf2image Pillow

import pytesseract
from pdf2image import convert_from_path
from docx import Document
from urllib.request import urlretrieve
import os
import re


pytesseract.pytesseract.tesseract_cmd = "/usr/bin/tesseract"

import pytesseract
from pdf2image import convert_from_path
from docx import Document
import re

pytesseract.pytesseract.tesseract_cmd = "/usr/bin/tesseract"

def scanned_pdf_to_word_local(pdf_path, output_docx):
    print("Using uploaded PDF:", pdf_path)

    pages = convert_from_path(pdf_path)
    print(f"Total pages found: {len(pages)}")

    doc = Document()

    for i, page in enumerate(pages):
        text = pytesseract.image_to_string(page)

        text = text.replace("\x0c", "")
        text = re.sub(r'[\x00-\x08\x0b\x0e-\x1f]', '', text)

        doc.add_heading(f"Page {i+1}", level=2)
        doc.add_paragraph(text)

        print(f"OCR completed for page {i+1}")

    doc.save(output_docx)
    print("Word document created:", output_docx)



