<template>
  <div>
    <h1>Google Drive PDF Open/Download</h1>
    <button @click="downloadPdfFromDrive(false)">Open PDF</button>
    <button @click="downloadPdfFromDrive(true)">Download PDF</button>
  </div>
</template>

<script>
export default {
  methods: {
    downloadPdfFromDrive(isDownload) {
      const fileId = "13nrItpG_p_evAkfzUO2zd-FcViXprXx1"; // Your Google Drive file ID
      const downloadUrl = `https://drive.google.com/uc?export=download&id=${fileId}`;

      const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);

      if (isDownload) {
        if (isSafari) {
          window.open(downloadUrl, "_blank"); // Safari opens, then user saves
        } else {
          const link = document.createElement('a');
          link.href = downloadUrl;
          link.download = "document.pdf"; // Download filename
          document.body.appendChild(link);
          link.click();
          document.body.removeChild(link);
        }
      } else {
        window.open(downloadUrl, "_blank"); // Open in new tab
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
