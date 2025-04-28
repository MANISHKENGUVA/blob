<template>
  <div>
    <h1>Dummy PDF Generator</h1>
    <button @click="createDummyPdf(false)">Open Dummy PDF</button>
    <button @click="createDummyPdf(true)">Download Dummy PDF</button>
  </div>
</template>

<script>
import Certificate from "./"
export default {
  methods: {
    async createDummyPdf(isDownload) {
      try {
        // 1. Create dummy content
        const dummyText = "This is a dummy PDF generated without API.";

        // 2. Create a Blob with PDF MIME type
        const pdfBlob = new Blob(, { type: "application/pdf" });

        // 3. Create a URL for the blob
        const blobURL = URL.createObjectURL(pdfBlob);

        // 4. Open or download the blob
        if (isDownload) {
          const link = document.createElement("a");
          link.href = blobURL;
          link.download = "dummy.pdf"; // file name
          document.body.appendChild(link);
          link.click();
          document.body.removeChild(link);
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
