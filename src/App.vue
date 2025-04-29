<!-- <template>
  <div>
    <h1>File Operations</h1>
    <input type="file" ref="fileInput" @change="handleFileUpload" style="display: none" />
    <button @click="triggerFileInput">Upload File</button>
    <button @click="downloadFile">Download File</button>
    <p v-if="fileMetadata">
      <strong>File Name:</strong> {{ fileMetadata.name }} <br />
      <strong>File Type:</strong> {{ fileMetadata.type }} <br />
      <strong>File Size:</strong> {{ fileMetadata.size }} bytes <br />
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fileMetadata: null,
    };
  },
  methods: {
    // Triggering hidden file input
    triggerFileInput() {
      this.$refs.fileInput.click();
    },
    // Handling file upload
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        this.fileMetadata = {
          name: file.name,
          type: file.type,
          size: file.size,
          lastModified: new Date(file.lastModified),
        };
      }
    },
    // Downloading file
    downloadFile() {
      const content = "Sample text content for download";
      const mime = "text/plain";
      const blob = new Blob([content], { type: mime });
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = "sample.txt";
      link.click();
      URL.revokeObjectURL(link.href);
    },
  },
};
</script>

<style scoped>
button {
  margin: 5px;
  padding: 10px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #45a049;
}
</style> -->


<!-- <template>
  <div>
    <h1>File Operations</h1>


    <input type="file" ref="fileInput" @change="handleFileUpload" style="display: none" />


    <button @click="triggerFileInput">Upload File</button>
    <button @click="downloadFile">Download File</button>

    <div v-if="fileMetadata">
      <h3>Uploaded File Metadata</h3>
      <p><strong>Name:</strong> {{ fileMetadata.name }}</p>
      <p><strong>Type:</strong> {{ fileMetadata.type }}</p>
      <p><strong>Size:</strong> {{ fileMetadata.size }} bytes</p>
      <p><strong>Last Modified:</strong> {{ fileMetadata.lastModified }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fileMetadata: null, // Metadata of the uploaded file
    };
  },
  methods: {
    // Trigger hidden file input for upload
    triggerFileInput() {
      this.$refs.fileInput.click();
    },

    // Handle file upload and extract metadata
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        this.fileMetadata = {
          name: file.name,
          type: file.type,
          size: file.size,
          lastModified: new Date(file.lastModified).toLocaleString(),
        };
      }
    },

    // Download a sample file
    downloadFile() {
      const content = "This is a sample text file.";
      const mime = "text/plain";
      const blob = new Blob([content], { type: mime });
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = "sample.txt";
      link.click();
      URL.revokeObjectURL(link.href);
    },
  },
};
</script>

<style scoped>

button {
  margin: 10px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}

/* Metadata display styling */
div {
  margin-top: 20px;
}
</style> -->


<template>
  <div>
    <button @click="downloadPdf">Download MEAN Stack Lab Manual</button>
  </div>
</template>

<script>
export default {
  name: 'DownloadPdfButton',
  data() {
    return {
      pdfUrl: 'https://github.com/MANISHKENGUVA/MEANSTACKLAB/raw/main/MEANSTACK%20LAB%20MANUAL%202022-23%201%20(1).pdf',
      pdfFileName: 'MEAN_STACK_LAB_MANUAL.pdf'
    };
  },
  methods: {
    downloadPdf() {
      const link = document.createElement('a');
      link.href = this.pdfUrl;
      link.download = this.pdfFileName;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
};
</script>
