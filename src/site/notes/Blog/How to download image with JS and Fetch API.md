---
{"dg-publish":true,"permalink":"/blog/how-to-download-image-with-js-and-fetch-api/","tags":"gardenEntry"}
---


First, make sure that response has 'Content-Disposition' header.

```javascript
function downloadImage(url) {
  fetch(url).then(res => {
    if(res.ok) {
      return res.blob(); // returns promise of blob
    } else {
      throw Error(res);
    }
  }).then(blob => {
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.target = "_parent";
    a.style.display = "none";
    document.body.appendChild(a);
    a.click();
    window.URL.revokeObjectURL(url);
    a!.parentNode!.removeChild(a);
  }).catch((err)=> {
    //handle error
  })
```