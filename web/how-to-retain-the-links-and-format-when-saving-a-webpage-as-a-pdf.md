# July 23, 2023 TIL - How to Retain the Links and Format when Saving a Webpage as a PDF

To save a webpage as a PDF while retaining the links and formatting, use the following steps:

1. Download/Install "SingleFile" browser extension
  - [SingleFile - Chrome Web Store](https://chrome.google.com/webstore/detail/singlefile/mpiodijhokgodhhofbcjdecpffjipkle)
  - [SingleFile – Firefox Add-On](https://addons.mozilla.org/en-US/firefox/addon/single-file/)
2. Configure "SingleFile" with the following options which may directly impact the format of the generated PDF (save yourself the headache and match your configurations to the ones below):
  1. HTML content
    - compress HTML content                    : true
    - remove hidden elements                   : true
    - set content security policy              : false
    - remove frames                            : true
    - save original URLs of embedded resources : true
    - do not include the saved date            : true
    - save raw page                            : false
  2. Infobar
    - display an infobar when viewing a saved page: false
  3. Stylesheets
    - remove unused styles                                    : false
    - remove stylesheets for alternative devices to screens   : true
    - compress CSS content                                    : false
    - move in the head element the styles found outside of it : true
  4. Images
    - group duplicate images together                  : true
    - save deferred images                             : true
    - dispatch "scroll" event                          : false
    - zoom out the page                                : false
    - remove images for alternative screen resolutions : true
  5. Fonts
    - remove unused fonts      : false
    - remove alternative fonts : false
  6. Network
    - blocked resources
      - images                                                 : false
      - stylesheets                                            : false
      - fonts                                                  : false
      - scripts                                                : true
      - videos                                                 : true
      - audios                                                 : true
    - block mixed content                                      : false
    - pass "Referer" header after a cross-origin request error : true
  7. Annotation editor
    - default mode                                              : normal
    - apply the system theme when formatting a page             : true
    - warn if leaving page with unsaved changes                 : true
    - annotate the page before saving                           : false
    - open pages saved with Singlefile in the annotation editor : false
3. Navigate to a webpage you want to save as a PDF (use Firefox as some browsers like Brave may not load certain resources needed to display graph/chart data correctly)
4. Ensure other styles injecting extensions are disabled and click the "SingleFile" icon to save the current webpage and resources as a single HTML file
5. Open the downloaded `webpage.html` in Brave or similar (Firefox may not preserve links in the generated PDF correctly)
6. Print the webpage and set the destination to "Save as PDF"
7. Open and view the downloaded `webpage.pdf` which should look fairly similar to the original webpage with working embedded links

## Use Cases

- Save a webpage as a PDF while retaining the original webpage format and with working links

