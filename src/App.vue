<template>
  <div>
    <h1>Download Dummy PDF from Google Drive</h1>
    <button @click="downloadFromDrive">Download PDF</button>
  </div>
</template>

<script>
export default {
  methods: {
    downloadFromDrive() {
      // Google Drive file ID from the URL you provided
      const fileId = "13nrItpG_p_evAkfzUO2zd-FcViXprXx1";  // Your File ID
      const downloadUrl = `https://drive.google.com/uc?export=download&id=${fileId}`;

      // Check if the browser is Safari
      const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);

      // If it's Safari, open in a new tab
      if (isSafari) {
        window.open(downloadUrl, "_blank");
      } else {
        // If not Safari, use the standard download method
        const link = document.createElement("a");
        link.href = downloadUrl;
        link.download = "dummy.pdf"; // The name you want the file to have when downloaded
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
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
