# js-bookmarklets
A collection of custom bookmarklets created by me

## How to add Bookmarklets

1. Open your bookmarks bar (Ctrl+Shift+B in Chrome/Edge/Firefox to toggle it)
2. Right-click the bookmarks bar and select Add page or New bookmark
3. Give it a name (e.g. "Google Maps Full Size Photo Extractor")
4. Paste the JavaScript code into the URL field instead of a web address
5. Click Save - it'll appear as a clickable button in your bar

## Google Maps Full Size Photo Extractor

Opens photos from the Google Maps Photo Gallery at their original upload quality and opens the highest resolution of whatever static angle and view of a 360° photo has been selected by the Maps viewer.

```javascript
javascript:(function(){const m=decodeURIComponent(location.href).match(/!6s(https:\/\/lh3\.googleusercontent\.com\/[^!]+)/);if(m){const u=m[1].replace(/=w\d+-h\d+-k-no/,"=s0-k-no");const w=window.open("","_blank");w.document.write('<title>Loading Image...</title><style>body{background:#111;display:flex;align-items:center;justify-content:center;height:100vh;margin:0}.loader{border:5px%20solid%20#333;border-top:5px%20solid%20#3498db;border-radius:50%;width:50px;height:50px;animation:spin%201s%20linear%20infinite}@keyframes%20spin{0%{transform:rotate(0)}100%{transform:rotate(360deg)}}%3C/style%3E%3Cdiv%20class=%22loader%22%3E%3C/div%3E');w.location.href=u;}else%20alert(%22No%20image%20URL%20found%20in%20current%20URL%22);})();
```

## Google Maps Full Size Video Extractor

Opens the selected video from the Google Maps Video Gallery in-browser, to watch in it's original resolution, as well as providing a download button to save it with the filename it was originally uploaded with by the user.

```javascript
javascript:(function(){const match=decodeURIComponent(window.location.href).match(/!6s(https:\/\/lh3\.googleusercontent\.com\/[^!]+)/);if(!match){alert("No video URL found in current URL");return;}const url=match[1].replace(/=w\d+-h\d+-k-no/,"=dv");const newWin=window.open("","_blank");newWin.document.write(`<title>Loading Video...</title><style>body{background:#111;display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:100vh;margin:0;gap:16px;color:#aaa;font-family:sans-serif;}video{max-width:100%;max-height:90vh;outline:none;}.download-btn{display:inline-block;padding:10px%2024px;background:#3498db;color:#fff;text-decoration:none;border-radius:6px;font-size:15px;margin-bottom:24px;}.download-btn:hover{background:#2980b9;}.error{color:#e74c3c;}%3C/style%3E%3Cscript%3Efetch(%22${url}%22,{mode:%22cors%22}).then(r=%3E{if(!r.ok)throw%20new%20Error(%22Fetch%20failed:%20%22+r.status);return%20r.blob();}).then(blob=%3E{const%20b=URL.createObjectURL(blob);const%20v=document.createElement(%22video%22);v.controls=true;v.autoplay=true;v.src=b;const%20a=document.createElement(%22a%22);a.href=%22${url}%22;a.textContent=%22%E2%AC%87%20Download%20Video%22;a.className=%22download-btn%22;document.body.innerHTML=%22%22;document.body.appendChild(v);document.body.appendChild(a);}).catch(err=%3E{document.body.innerHTML=%22%3Cp%20class='error'%3EFailed%20to%20load%20video:%20%22+err.message+%22%3Cbr%3ECORS%20may%20be%20blocking%20the%20request%20or%20the%20file%20is%20not%20a%20video.%3C\/p%3E%22;});%3C\/script%3E%3Cp%3EFetching%20video...%3C/p%3E%60);})();
```
