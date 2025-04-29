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


<!-- <template>
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
</script> -->


<!-- <template>
  <div>
    <button @click="downloadJson">Download JSON</button>
  </div>
</template>

<script>
export default {
  name: 'DownloadJsonButton',
  methods: {
    downloadJson() {
      const jsonObject = { name: "John", age: 30, car: null };

      // Convert to JSON string with indentation
      const jsonString = JSON.stringify(jsonObject, null, 2);

      // Create a Blob
      const blob = new Blob([jsonString], { type: "application/json" });

      // Create a temporary download link
      const link = document.createElement("a");
      link.download = "file.json";
      link.href = URL.createObjectURL(blob);

      // Trigger the download
      link.click();

      // Optional: Revoke object URL to release memory
      URL.revokeObjectURL(link.href);
    }
  }
};
</script> -->



<template>
  <div>
    <button @click="downloadPdf('SALE_AGREEMENT', 'MEAN_STACK_LAB_MANUAL.pdf')">Download PDF</button>
  </div>
</template>

<script>
export default {
  name: 'DownloadPdfButton',
  methods: {
    async downloadPdf(doctype, name) {
      let type;
      if (doctype === "SALE_AGREEMENT") {
        type = "saleagreement";
      } else if (doctype === "COC") {
        type = "projectcompletion";
      } else {
        type = "loandocs";
      }

      const params = {
        loanId: doctype === "COC" ? this.invoiceId : this.$route.query.loanId,
        type: type,
        imagedesc: doctype,
        name: name,
      };

      try {
        // Fake API response simulation (base64 encoded PDF)
        const res = await this.simulateApiCall(params);

        // Get base64-encoded PDF data from the response
        const base64Data = res.data;

        // Decode base64 to binary
        const binaryData = atob(base64Data);
        const arrayBuffer = new ArrayBuffer(binaryData.length);
        const byteArray = new Uint8Array(arrayBuffer);
        for (let i = 0; i < binaryData.length; i++) {
          byteArray[i] = binaryData.charCodeAt(i);
        }

        // Create Blob from binary data
        const blob = new Blob([byteArray], { type: 'application/pdf' });
        const url = window.URL.createObjectURL(blob);

        // Detect Safari and handle file download accordingly
        const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);
        
        if (isSafari) {
          // Open in a new tab for Safari
          const newTab = window.open();
          if (newTab) {
            newTab.location.href = url;
          } else {
            // Fallback if popup is blocked
            window.location.href = url;
          }
        } else {
          // For other browsers (Chrome, Firefox, etc.)
          const a = document.createElement('a');
          a.href = url;
          a.download = name;
          document.body.appendChild(a);
          a.click();
          document.body.removeChild(a);
          setTimeout(() => URL.revokeObjectURL(url), 3000);  // Clean up URL object
        }
      } catch (error) {
        console.error('Download failed', error);
      }
    },

    // Fake API call simulation
    simulateApiCall(params) {
      return new Promise((resolve) => {
        setTimeout(() => {
          // Simulate a fake base64-encoded PDF response (shortened for example purposes)
          const fakeBase64Pdf = 'JVBERi0xLjQKJeLjz8MKNjEwM......';  // Replace with actual base64 string

          resolve({
            data: fakeBase64Pdf,
          });
        }, 1000);  // Simulate network delay
      });
    }
  }
};
</script>

