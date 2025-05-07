# Ring Alarm Event History Export to CSV
# Bookmarklet Maker

Create your own bookmarklets easily using this browser-based tool.

## 🚀 Features

- Write JavaScript and instantly convert it to a bookmarklet
- Get both the encoded `javascript:` link and an embeddable HTML snippet
- Preloaded with an example: **Ring.com CSV Exporter**
- Run your JavaScript on the page to test live
- Fully client-side — no uploads or tracking

## 📦 How to Use

1. Open `index.html` in your browser.
2. Edit the title and JavaScript code.
3. Click **Generate Bookmarklet**.
4. Drag the generated blue link to your browser’s bookmarks bar.

## 💡 Example Bookmarklet

The default example extracts event data from a `.event-row` table on a Ring-style dashboard, formats it to CSV, and triggers a file download.

```js
(function() {
  let csv = 'date,time,description\\n';
  document.querySelectorAll('.event-row').forEach(row => {
    const date = row.querySelector('.date')?.innerText || '';
    const time = row.querySelector('.time')?.innerText || '';
    const desc = row.querySelector('.desc')?.innerText || '';
    csv += `"${date}","${time}","${desc}"\\n`;
  });
  const blob = new Blob([csv], { type: 'text/csv' });
  const link = document.createElement('a');
  link.href = URL.createObjectURL(blob);
  link.download = 'ring-events.csv';
  link.click();
})();

