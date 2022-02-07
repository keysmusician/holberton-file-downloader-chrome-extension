# Holberton File Downloader
The fast and convenient way to create Holberton School project files.

https://user-images.githubusercontent.com/74752740/149923346-53565e75-fcad-4adb-8b1c-42f2dd33d601.mov

## About
Holberton File Downloader is a browser extension which downloads project files from file names scraped from the active Holberton School project web page. "Main" files are downloaded containing their contents, while other files are blank. Holberton File Downloader is an alternative to [hb-file-creator](https://github.com/tieje/hb-file-creator) by [@Tieje](https://github.com/tieje).

## Installation

### Web Stores
The easiest way to install Holberton File Downloader is from either the Chrome Web Store or Firefox Add-on store:

https://chrome.google.com/webstore/detail/holberton-file-downloader/lknkfkffdokfodgfmcblomakemcbgomp

https://addons.mozilla.org/en-US/firefox/addon/holberton-file-downloader/

#### Enhanced Safe Browsing warning
<img width="448" alt="Screen Shot 2022-01-18 at 7 43 02 PM" src="https://user-images.githubusercontent.com/74752740/150042101-2f2d0a15-762e-40e1-8f64-40deeed5f84b.png">
If you see a warning that the extension is not trusted by Enhanced Safe Browsing, simply click "Continue to install." The warning is displayed because my developer account is new and has not yet received trusted status, which can take a few months. Rest assured that the extension collects no data and is capable of doing nothing except downloading files scraped from the active Holberton School project page. Feel free to browse the source code to verify the safety.


### Manual Unpacked Installation
Alternatively, Holberton File Downloader may be installed manually and loaded unpacked. This can be useful if you wish to modify the extension.

#### Chrome:
1) Download the extension folder (by cloning this repository)
2) Navigate to `chrome://extensions/`
3) Enable Developer mode, then click "load unpacked," and select the extension folder (called "Holberton File Downloader")
<div align="center">
  <img src=https://wd.imgix.net/image/BhuKGJaIeLNPW9ehns59NfwqKxF2/vOu7iPbaapkALed96rzN.png>

  <p><em>Source: https://developer.chrome.com/docs/extensions/mv3/getstarted/#manifest</em></p>
</div>

#### Firefox:
1) Download the extension folder (by cloning this repository)
2) In Firefox, navigate to `about:debugging#/runtime/this-firefox`
3) Click "Load Temporary Add-on..." and select a file in the same folder as `manifest.json`
<div align="center">
<img width="713" alt="Screen Shot 2022-01-31 at 12 03 25 AM" src="https://user-images.githubusercontent.com/74752740/151741908-d7e8ddec-fbc6-454c-b22f-4c10a4bf7e6c.png">
</div>

That's it! The extension is installed.

## Usage

To download files, navigate to any Holberton School project page, click the extension icon, then "Find files," then "Download" (or "Download as..." to choose the download location). The extension is only active on `intranet.hbtn.io`.  If you were already viewing a project when you installed the extension, refresh the page.

## Comparison
| Category | Holberton File Downloader | hb-file-creator |
|---|---|---|
| Installation/setup | Install from a web store, or download from this repo and load the extension. See [Installation](#installation) above. | Download the script, a compatible Chrome driver, Python and Selenium as needed. Configure your username & password in a JSON file, and alias the script. |
| Usage | Visit any project page, then click "Find files", then "Download." | Type `hb <holberton_project_url>` + <return\>|
| Browser Compatibility | Chrome, Firefox | Chrome |
| File destination | Any local directory | Any local directory |
| Interface | GUI (HTML) | Command line (works inside a VM) |

## To do

- [ ] Merge Chrome and Firefox folders so both share files
- [ ] Include toggleable contents by file extension:
  - [ ] Shebangs, where appropriate. ~~The downside of this is that Chrome detects these as executable scripts and issues a warning when downloading~~ (this is no longer an issue with the adoption of .zip files).
  - [ ] Header guards in header files (\*.h)
  - [ ] Custom user-specified templates (README.md, \*.py, etc.)
- [ ] UI
  - [ ] Display files in a tree structure
  - [ ] Prettier interface/CSS
  - [ ] Dark mode
- [ ] Add a privacy policy
- [x] ~~Search upon clicking the extension instead of clicking "Find files."~~
- [x] ~~Cross browser compatibility~~ Supports Firefox 1/28/22
- [x] ~~Scrape main files~~
- [x] ~~Use [Chrome's download/save dialog](https://developer.chrome.com/docs/extensions/reference/downloads/#method-download) to specify download location~~ Done 1/18/22
- [x] ~~Arrange files in the correct subdirectories~~
- [x] ~~Sometimes filenames (header files for C projects) appear in the "Requirements" section. These could be included as well.~~
- [x] ~~Correctly name the project directory~~


## Bugs
- ~~If `cat -e` is used, the files are skipped, but they should be downloaded without the trailing `$`~~
- ~~If there are multiple `cat`ted files with the same name, the first should be downloaded rather than the last; Don't overwrite.~~
- ~~README.md and header files should be placed in the root directory absent a "0x" project folder.~~
- ~~Project titles containing forward slashes result in treating the title as a path and creating a directory due to the illegal file name character.~~
- ~~Blank files are created for non-text file extensions (e.g., .jpg, .so, .a ).~~
- ~~A `cat` invocation followed by a bash redirect results in the redirect command being included in the file name.~~
- ~~File names containing escaped spaces get downloaded with the backslashes in the file name.~~
- ~~Regex which determines when to stop scraping main/header file content was typed incorrectly and consequently can be "tricked" into terminating early.~~
- ~~Files given from absolute paths should be ignored. This is because we assume that if a file is in the PWD or close to it, it will be `cat`ted with a relative path. Additionally, files using an absolute path are likely system files which already exist, or otherwise do not need to be downloaded.~~
- ~~File names which include directories such as `dir/file.txt` get downloaded with the slashes converted to underscores, as in `dir_file.txt`. The extension ideally should create the necessary directories.~~ Fixed 1/14/21
- ~~Some files have downloaded with a leading underscore. This may be caused by whitespace or an invisible character.~~ Fixed 1/14/22
- ~~Additionally, all the files should be placed within a single directory rather than downloaded individually to the Chrome downloads location.~~ Fixed 1/13/22
- ~~Only downloads the first 10 files~~ Fixed 1/13/22

### Limitations
Currently, the string `$ cat ` is used to determine if a file in the task-card section of the project page ought to be scraped. This has the disadvantage of missing any files with more than one space after the `$`. It could be improved by using a regular expression, but this has yet to be an issue.

Use of `cat -e` is considered and the trailing `$` are stripped. Use of other options is unlikely, and modifies the output in more complex ways, so such files are skipped.

If `$ cat ` is used to cat more than one file, it would be difficult to tell where one file ends and the next begins. The current behavior would consider the entire output of `cat` to belong to the first file that was `cat`ted. However, it is unlikely there will be a real situation where multiple files are `cat`ted in a project task card.

Occasionally, a project may `cat` a file that doesn't need to be downloaded. In this case the simplest solution is to just delete the file, since it's much more difficult to get Holberton File Downloader to determine if a file is relevant or not.
