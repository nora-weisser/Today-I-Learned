### Validate Downloaded CSV File using Playwright

1. Start waiting for download before clicking. Note: no await.
```
const downloadPromise = page.waitForEvent(‘download’);
await page.getByText(‘Download file’).click();
const download = await downloadPromise;
```
2. Wait for the download process to complete and save the downloaded file somewhere.

```
await download.saveAs(‘/path/to/save/at/’ + download.suggestedFilename());
```
3. Validate content of the file using css-parser library.

```
async validateTableInCSV(download: Download) {
    const filePath = ‘test-data/downloads/<folder>/’ + download.suggestedFilename();
    const readStream = fs.createReadStream(filePath);
    let isFirstRowProcessed = false;
    readStream
      .pipe(csvParser())
      .on(‘headers’, (headers: string[]) => {
        console.log(‘CSV Headers:‘, headers);
        const headersStr = headers[0];
        expect(headers[0].split(<delimeter>)).toEqual(<expected headers>)
      })
      .on(‘error’, (error: Error) => {
        console.error(‘Error:’, error);
      })
      .on(‘data’, (row: object) => {
        if (!isFirstRowProcessed) {
         console.log(‘First Row Data:’, row);
         isFirstRowProcessed = true;
         readStream.destroy();
        }
       })
      .on(‘end’, () => {
        console.log(‘CSV parsing finished’);
      });
  }
```
