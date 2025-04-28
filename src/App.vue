<template>
  <div>
    <h1>Dummy PDF Generator (Working on Safari, Chrome, Firefox)</h1>
    <button @click="createDummyPdf(false)">Open Dummy PDF</button>
    <button @click="createDummyPdf(true)">Download Dummy PDF</button>
  </div>
</template>

<script>
export default {
  methods: {
    createDummyPdf(isDownload) {
      try {
        // 1. Very minimal valid PDF structure
        const pdfContent = `%PDF-1.4
1 0 obj
<< /Type /Catalog /Pages 2 0 R >>
endobj
2 0 obj
<< /Type /Pages /Kids [3 0 R] /Count 1 >>
endobj
3 0 obj
<< /Type /Page /Parent 2 0 R /MediaBox [0 0 612 792] /Contents 4 0 R /Resources << >> >>
endobj
4 0 obj
<< /Length 44 >>
stream
BT
/F1 24 Tf
100 700 Td
(Dummy PDF) Tj
ET
endstream
endobj
xref
0 5
0000000000 65535 f 
0000000010 00000 n 
0000000060 00000 n 
0000000117 00000 n 
0000000213 00000 n 
trailer
<< /Root 1 0 R /Size 5 >>
startxref
312
%%EOF`;

        // 2. Convert to bytes
        const byteCharacters = unescape(encodeURIComponent(pdfContent));
        const byteNumbers = new Array(byteCharacters.length);
        for (let i = 0; i < byteCharacters.length; i++) {
          byteNumbers[i] = byteCharacters.charCodeAt(i);
        }
        const byteArray = new Uint8Array(byteNumbers);

        // 3. Create Blob
        const pdfBlob = new Blob([byteArray], { type: "application/pdf" });

        // 4. Create Blob URL
        const blobURL = URL.createObjectURL(pdfBlob);

        // 5. Detect if browser is Safari
        const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);

        if (isDownload) {
          if (isSafari) {
            // Safari doesn't support link.download with blob URLs very well
            // Instead, open it and let user manually save
            window.open(blobURL, "_blank");
          } else {
            const link = document.createElement("a");
            link.href = blobURL;
            link.download = "dummy.pdf"; // filename
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
          }
        } else {
          window.open(blobURL, "_blank");
        }
      } catch (error) {
        console.error("Error creating dummy PDF:", error);
      }
    }
  }
};
</script>

<style scoped>
button {
  margin: 10px;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 5px;
}
button:hover {
  background-color: #45a049;
}
</style>
