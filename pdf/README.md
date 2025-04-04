How To Create PDF (on macOS)
============================


Setup
-----
* Install Adobe Acrobat Pro DC.
* Copy headers and footers from `pdf/acrobat/` folder to `/Users/<username>/Library/Preferences/Adobe/Acrobat/DC/HeaderFooter/`.


Printing to PDF
---------------
### Normal PDF
* Open `index.html` in text editor and first remove element `<p><br></p>` before the `<h1>Libraries</h1>`.
* Then replace the index and footer with contents of `pdf/index_for_pdf.html` file and save.
* Disable internet connection and open Chromium version 108.0.5328.0 (later versions will render the site incorrectly after index is added). Right click anywhere in the window and choose 'inspect'. Go to 'Network' tab and check 'Disable Cache'. Open the `index.html` file while keeping the inspect window open.
* Right click on the border of the site and select inspect. Select `<body>` element under 'Elements' tab and change top margin and top padding from 16 to 0 in 'Styles' tab.
* Change brightness of comments by right clicking on one of them and selecting inspect. Then click on the rectangle that represents color and toggle the color space to HSLA by clicking on the button with two vertical arrows. Change lightness (L) percentage to 77%.
* Change the brightness of text to 13%.
* Select 'Print...' with destination 'Save as PDF', paper size 'A4', 'Default' margins (top 10mm, right 9.5mm, bottom 8mm and left 10mm), 'Default' scale and no headers and footers and save (the document should be 51 pages long with last page empty).
* Check if plots were rendered correctly.

### PDF optimized for laser color printing
* Run `./parse.js` again.
* Change all links in text to normal text and add a page number in brackets like that: '(p. <page_num>)' by running './pdf/remove_links.py' (Links can be found with this regex: `<strong>.*a href.*</strong>`).
* Open `index.html` in text editor and first remove element `<p><br></p>` before the `<h1>Libraries</h1>`.
* Then replace the index and footer with contents of `pdf/index_for_pdf_print.html` file and save.
* Disable internet connection and open Chromium version 108.0.5328.0 (later versions will render the site incorrectly after index is added). Right click anywhere in the window and choose 'inspect'. Go to 'Network' tab and check 'Disable Cache'. Open the `index.html` file while keeping the inspect window open.
* Right click on the border of the site and select inspect. Select `<body>` element under 'Elements' tab and change top margin and top padding from 16 to 0 in 'Styles' tab.
* Change brightness of elements by right clicking on them and selecting inspect. Then click on the rectangle that represents color and toggle the color space to HSLA by clicking on the button with two vertical arrows.
* Change lightness (L) percentage to:
* 0% for the text.
* 87% for the gray line on the left side of the code.
* 89% for the gray hash characters by the titles
* 37% for the red text and function names (they use their own red).
* 60% for the blue text and the text in the contents (it uses its own blue), but leave color of decorators and the `>>>` intact.
* 58% for the comments.
* Individually change brightness of every comment line that starts with: `# $ pip3 install` and of comments in basic script template to 57%, by adding `color: hsla(0, 0%, 57%, 1);` to their element.style.
* Select 'Print...' with destination 'Save as PDF', paper size 'A4', 'Default' margins (top 10mm, right 9.5mm, bottom 8mm and left 10mm), 'Default' scale and no headers and footers and save (the document should be 51 pages long with last page empty).
* Check if plots were rendered correctly.


Adding headers and footers to PDF (the same for both files)
-----------------------------------------------------------
* Open the PDF file in Adobe Acrobat Pro DC.
* Select 'Organize Pages'.
* Right click the second page and select 'Crop Pages...'.
* Select units: 'Inches'.
* In 'Change page size' section select 'A4' for 'Page Sizes' and set 'XOffset' to '0.1 in'. Then click on 'YOffset' input field, so the x offset gets registered. Select page range 'All' and click OK.
* Select 'Edit PDF' tab and add headers and footers by clicking 'Header & Footer' button, selecting a preset from 'Saved Settings' dropdown menu and clicking ok. Popup will say that font 'Menlo' contains invalid encoding. This is fine.
* Start by adding the bottom_line preset and check afterward if bottom line on the first page is aligned properly with the text. If it is not close the file and start over.
* Repeat the process for each preset. When popup asks you if you want to replace existing header or footer click 'Add New'.
* Use this values for font and margins if presets get lost: Borders: left-line: 0.6, left-text: 0.8, top-line: 11.4, bottom-text: 0.27, right-text-odd: 0.57, font-name: menlo, font-size: 8.
* Select 'Organize Pages' tab and remove the last page (it should be empty).
* Select 'File/Properties...' and set title to 'Comprehensive Python Cheatsheet' and author to 'Jure Šorn'.
* Save the progress by running 'Save as' in Format: 'Adobe PDF Files'.
* Run 'Save as' again, this time in 'Adobe PDF Files, Optimized', so that Menlo font error gets fixed.


Compressing
-----------
* Compress the two files together with HOW_TO_PRINT.txt instruction file that contains the instructions from the next section using: `zip 'Comprehensive Python Cheatsheet.zip' 'Comprehensive Python Cheatsheet.pdf' 'Comprehensive Python Cheatsheet (optimized for printing).pdf' 'HOW_TO_PRINT.txt'`.


Printing the PDF
----------------
* Open the PDF that was optimized for printing in Chrome and print on A4 on both sides with default margins, scale 98% and no headers and footers.
