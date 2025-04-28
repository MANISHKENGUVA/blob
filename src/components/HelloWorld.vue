<template>
  <div class="container">
    <h1>Dummy PDF Generator</h1>

    <!-- Basic Blob PDF -->
    <button @click="createDummyPdf(false)">Open Dummy PDF (Basic)</button>
    <button @click="createDummyPdf(true)">Download Dummy PDF (Basic)</button>

    <hr />

    <!-- jsPDF Generated PDF -->
    <button @click="createDummyPdfUsingJsPDF(false)">
      Open Dummy PDF (jsPDF)
    </button>
    <button @click="createDummyPdfUsingJsPDF(true)">
      Download Dummy PDF (jsPDF)
    </button>
  </div>
</template>

<script>
import { jsPDF } from 'jspdf';

export default {
  name: 'DummyPdfGenerator',
  methods: {
    // Basic method using Blob
    createDummyPdf(isDownload) {
      const dummyText = 'This is a dummy PDF generated without an API call.';

      const pdfBlob = new Blob([dummyText], { type: 'application/pdf' });
      const blobURL = URL.createObjectURL(pdfBlob);

      if (isDownload) {
        const link = document.createElement('a');
        link.href = blobURL;
        link.download = 'dummy-basic.pdf'; // File name for download
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
      } else {
        window.open(blobURL, '_blank');
      }
    },

    // Better method using jsPDF
    createDummyPdfUsingJsPDF(isDownload) {
      const doc = new jsPDF();
      doc.text('This is a properly generated PDF using jsPDF!', 10, 10);

      if (isDownload) {
        doc.save('dummy-jsPDF.pdf');
      } else {
        const blob = doc.output('blob');
        const blobURL = URL.createObjectURL(blob);
        window.open(blobURL, '_blank');
      }
    },
  },
};
</script>

<style scoped>
.container {
  padding: 20px;
}

button {
  margin: 10px;
  padding: 10px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

h1 {
  margin-bottom: 20px;
}
</style>
