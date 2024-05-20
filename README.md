## Overview

Overview
ChromeExtension is a project designed to facilitate communication between a Chrome extension and a native application, focusing on event handling, message passing, and form options retrieval. The extension interacts with a native application to validate and manage specific actions through communication ports.

##
## Features

Features
- Message passing between content scripts, background scripts, and a native application.
- Event handling and port management.
- Retrieval and management of form filling options.
- Integration with external libraries like jQuery.

##
## Installation Instructions

Installation Instructions
1. **Clone the Repository:**
   ```sh
   git clone https://github.com/laurenzlong/ChromeExtension.git
   ```
2. **Load the Extension:**
   - Open Chrome, navigate to `chrome://extensions/`.
   - Enable 'Developer mode' by clicking the toggle switch.
   - Click on 'Load unpacked' and select the `ChromeExtension` directory.

3. **Set up the Native Application:**
   - Navigate to `C:\Users\Yuriy\Documents\GitHub\ChromeExtension\NymiNativeMsgApp\NCLTestApp`.
   - Build the native application using your preferred C++ compiler.
   - Ensure the native messaging host is properly set up as defined by Chrome's [Native Messaging](https://developer.chrome.com/docs/apps/nativeMessaging/).

##
## Usage Examples

Usage Examples
### Starting the Extension
Once installed and loaded into Chrome, the extension will automatically start upon page load.

### Message Passing
- The content script sends a message to the background script:
  ```javascript
  chrome.runtime.sendMessage({
    "subject": "contentScript",
    "action": "getOptions",
    "condition": "authenticated",
    "args": [], 
    "note": "none"
  }, function(response) {
    console.log(response);
  });
  ```
- Example of `eventPage.js` handling a message:
  ```javascript
  chrome.runtime.onMessage.addListener(function(request, sender, sendResponse) {
    if (request.subject == "contentScript") {
      console.log('Getting options...');
      sendResponse(core.getOptions());
    }
  });
  ```

### Native Application Interaction
The native application handles provision messages and communicates with the extension:
```cpp
void sendMsgToChrome(string msg, string target) {
  cout << "Sending message to Chrome: " << msg << endl;
}
```

### Options Page Management
- Using jQuery to manage form options:
  ```javascript
  jQuery(function($) {
    var page = $('#options-page'); 
    var tpl = page.find('.template');
    tpl.hide();
    function createQuery(id) {
      // code to manage options...
    }
  });
  ```

##
## Code Summary

Code Summary
- **contentScript.js**: Handles content script logic, sends messages to the background script.
- **eventPage.js**: Background script for event handling, manages core logic and communication.
- **index.js**: Initializes port communication and validates events.
- **jquery-1.8.2.min.js**: Minified jQuery library for DOM manipulation.
- **options.js**: Manages the options page using jQuery.
- **NCLTestApp\NCLTestApp.cpp**: Native application for handling Nymi's communication messages.
- **NCLTestApp\stdafx.cpp**: Source file for standard includes and type information.

##
## License

License
This project is licensed under the MIT License. For more details, see the [LICENSE](LICENSE) file.

---

By following these instructions, you should be able to set up and use the `ChromeExtension` project efficiently. For further information or support, please check the code comments or contact the repository maintainer.