# Ring Alarm Event History Export to CSV

# Fast Easy Option 

Click the link in the About section above to the right and just drag the Blue "Ring Export" Button on to the bookmarks bar.

# Bookmarklet Maker

Create your own bookmarklets easily using this browser-based tool.

## 🚀 Features

- Write JavaScript and instantly convert it to a bookmarklet
- Get both the encoded `javascript:` link and an embeddable HTML snippet
- Preloaded with an example: **Ring.com CSV Exporter**
- Run your JavaScript on the page to test live
- Fully client-side — no uploads or tracking

## 📦 How to Use

1. Read the instructions below first before opening the generator (Hold Ctrl while clicking the link to open in a new tab).
2. Edit the title and JavaScript code.
3. Click **Generate Bookmarklet**.
4. Drag the generated blue link to your browser’s bookmarks bar. Open the [Bookmarklet-Generator](https://beattheforms.github.io/Ring_Alarm_Event_Export_to_CSV/bookmarklet-generator.html)

## 💡 Example Bookmarklet

The is the code already in the generator. It extracts event data from the Ring Event History and formats it to CSV, and triggers a file download.

```js
javascript:(() => {
  function escapeCSV(val) {
    return `"${(val || '').replace(/"/g, '""')}"`;
  }

  const items = Array.from(document.querySelectorAll('article[data-testid="event-item"]'));
  const rows = [['Device', 'Event', 'Date', 'Time']];

  items.forEach(item => {
    const device = item.querySelector('[class*="DeviceName"]').textContent.trim();
    const event = item.querySelector('[data-testid="event-item__event-kind"]').textContent.trim();
    const dateElems = item.querySelectorAll('[class*="DateTimeContainer"]');
    const date = dateElems[0]?.textContent.trim() || '';
    const time = dateElems[1]?.textContent.trim() || '';

    rows.push([device, event, date, time].map(escapeCSV));
  });

  const csvContent = rows.map(r => r.join(',')).join('\n');
  const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
  const link = document.createElement('a');
  link.href = URL.createObjectURL(blob);
  link.download = 'ring_event_history.csv';
  link.click();
})();


