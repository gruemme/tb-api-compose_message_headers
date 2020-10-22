# Compose Message Headers - Experimental Webextention API for Thunderbird

Experimental webextention api to modify message headers

There are the following functions:

* `browser.composeMessageHeaders.addComposeHeader(tabId, headerName, headerValue)` Sets the header with name *headerName* with the value *headerValue* in the message inside the *tabId*
* `browser.composeMessageHeaders.deleteComposeHeader(tabId, headerName)` Deletes the headerline of header with name *headerName* in the message inside the *tabId*
* `browser.composeMessageHeaders.hasComposeHeader(tabId, headerName)` If header with name *headerName* is present in the message inside the *tabId*
* `browser.composeMessageHeaders.getComposeHeader(tabId, headerName)` Gets the value of header with name *headerName* in the message inside the *tabId*



Example usage:
```
function setMyHeaderValue( event, tabId ) {
    if(event.target.value) {
      console.log('Set myheader header to: ' + event.target.value);
      browser.composeMessageHeaders.addComposeHeader(tabId, 'X-MYHEADER', event.target.value);
    } else {
      console.log('Remove myheader');
      browser.composeMessageHeaders.deleteComposeHeader(tabId, 'X-MYHEADER');
    }

    return false;
};


// Set onchange to a select in popup.html with id `input-headerid`
browser.tabs.query({
  active: true,
  currentWindow: true,
}).then(tabs => {
  let tabId = tabs[0].id;
  let input = document.getElementById("input-headerid");
  input.addEventListener("change", () => setMyHeaderValue(event, tabId)) ;
});
```

