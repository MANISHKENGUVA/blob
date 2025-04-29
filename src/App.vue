<template>
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
</style>