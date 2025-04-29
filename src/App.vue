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

<!-- 
<template>
  <div>
    <button @click="downloadPdf('SALE_AGREEMENT', 'MEAN_STACK_LAB_MANUAL.pdf')">Download PDF</button>
  </div>
</template>

<script>
async downloadPdf(doctype, name) {
  let type;
  if (doctype === "SALE_AGREEMENT") {
    type = "saleagreement";
  } else if (doctype === "COC") {
    type = "projectcompletion";
  } else {
    type = "loandocs";
  }

  const loanId = this.generateFakeLoanId();

  const params = {
    loanId: loanId,
    type: type,
    imagedesc: doctype,
    name: name,
  };

  try {
    // Detect Safari
    const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);
    let newTab;

    if (isSafari) {
      // Immediately open blank tab
      newTab = window.open('about:blank');
    }

    // Simulate API call
    const res = await this.simulateApiCall(params);
    const base64Data = res.data;

    const binaryData = atob(base64Data);
    const arrayBuffer = new ArrayBuffer(binaryData.length);
    const byteArray = new Uint8Array(arrayBuffer.length);
    for (let i = 0; i < binaryData.length; i++) {
      byteArray[i] = binaryData.charCodeAt(i);
    }

    const blob = new Blob([byteArray], { type: 'application/pdf' });
    const url = window.URL.createObjectURL(blob);

    if (isSafari) {
      if (newTab) {
        newTab.location.href = url;
      } else {
        window.location.href = url;
      }
    } else {
      const a = document.createElement('a');
      a.href = url;
      a.download = name;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      setTimeout(() => URL.revokeObjectURL(url), 3000);
    }
  } catch (error) {
    console.error('Download failed', error);
  }
}


</script> -->


<!-- <template>
  <div>
    <button @click="downloadPdf('SALE_AGREEMENT', 'Agreement.pdf')">Download PDF</button>
  </div>
</template>

<script>
export default {
  name: "App",
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

      const loanId = this.generateFakeLoanId();

      const params = {
        loanId: loanId,
        type: type,
        imagedesc: doctype,
        name: name,
      };

      try {
        const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);
        let newTab;
        if (isSafari) newTab = window.open("about:blank");

        const res = await this.simulateApiCall(params); // simulate dummy base64
        const base64Data = res.data;
        const binaryData = atob(base64Data);
        const arrayBuffer = new ArrayBuffer(binaryData.length);
        const byteArray = new Uint8Array(arrayBuffer);
        for (let i = 0; i < binaryData.length; i++) {
          byteArray[i] = binaryData.charCodeAt(i);
        }

        const blob = new Blob([byteArray], { type: "application/pdf" });
        const url = window.URL.createObjectURL(blob);

        if (isSafari) {
          if (newTab) {
            newTab.location.href = url;
          } else {
            window.location.href = url;
          }
        } else {
          const a = document.createElement("a");
          a.href = url;
          a.download = name;
          document.body.appendChild(a);
          a.click();
          document.body.removeChild(a);
          setTimeout(() => URL.revokeObjectURL(url), 3000);
        }
      } catch (error) {
        console.error("Download failed", error);
      }
    },

    generateFakeLoanId() {
      return "LOAN-" + Math.random().toString(36).substr(2, 9).toUpperCase();
    },

    simulateApiCall(params) {
      // returns fake base64 PDF data (1-page PDF)
      const dummyPdfBase64 =
        "JVBERi0xLjQKJeLjz9MKNCAwIG9iago8PC9UeXBlIC9QYWdlL1BhcmVudCAxIDAgUi9SZXNvdXJjZXMgMiAwIFIvTWVkaWFCb3hbMCAwIDYxMiA3OTJdL0NvbnRlbnRzIDUgMCBSL0dyb3VwPDwvUy9UcmFuc3BhcmVuY3kvQ1MvRGV2aWNlUkdCPj4+PgplbmRvYmoKNSAwIG9iago8PC9MZW5ndGggNjI+PnN0cmVhbQpCBiAgICAgICAgVGhpcyBpcyBhIGZha2UgcGRmIHJlc3BvbnNlIGZyb20gVmVlLgplbmRzdHJlYW0KZW5kb2JqCjYgMCBvYmoKPDwvVHlwZS9DYXRhbG9nL1BhZ2VzIDMgMCBSPj4KZW5kb2JqCjcgMCBvYmoKPDwvQ3JlYXRpb25EYXRlKEQ6MjAyNTA0MjkxMjA1MjIrMDAnMDAnKS9Nb2REYXRlKEQ6MjAyNTA0MjkxMjA1MjIrMDAnMDAnKT4+CmVuZG9iago4IDAgb2JqCjw8L1R5cGUvWE9iamVjdD4+CmVuZG9iagp4cmVmCjAgOQowMDAwMDAwMDAwIDY1NTM1IGYgCjAwMDAwMDAwMTAgMDAwMDAgbiAKMDAwMDAwMDAyNSAwMDAwMCBuIAowMDAwMDAwMDUwIDAwMDAwIG4gCjAwMDAwMDAxMjAgMDAwMDAgbiAKMDAwMDAwMDE1MCAwMDAwMCBuIAowMDAwMDAwMzAwIDAwMDAwIG4gCjAwMDAwMDAzNjAgMDAwMDAgbiAKMDAwMDAwMDQyMCAwMDAwMCBuIAp0cmFpbGVyCjw8L1Jvb3QgNiAwIFIvU2l6ZSA5Pj4Kc3RhcnR4cmVmCjQ0NQolJUVPRgo=";

      return new Promise((resolve) =>
        setTimeout(() => resolve({ data: dummyPdfBase64 }), 1000)
      );
    }
  }
};
</script> -->


<template>
  <div class="download-container">
    <button @click="DownloadLoanDocuments('SALE_AGREEMENT', 'SaleAgreement.pdf')">
      Download Sale Agreement
    </button>
    <button @click="DownloadLoanDocuments('COC', 'CompletionCertificate.pdf')">
      Download COC
    </button>
    <button @click="DownloadLoanDocuments('OTHER', 'LoanDocument.pdf')">
      Download Loan Docs
    </button>
  </div>
</template>

<script>
export default {
  name: "DownloadPdf",
  data() {
    return {
      invoiceId: "INV-123456", // Mocked for demo
    };
  },
  methods: {
    async DownloadLoanDocuments(doctype, name) {
      let type;
      if (doctype === "SALE_AGREEMENT") {
        type = "saleagreement";
      } else if (doctype === "COC") {
        type = "projectcompletion";
      } else {
        type = "loandocs";
      }

      const loanId =
        doctype === "COC"
          ? this.invoiceId
          : this.$route?.query?.loanId || "LOAN-" + Math.random().toString(36).substr(2, 8).toUpperCase();

      const params = {
        loanId: loanId,
        type: type,
        imagedesc: doctype,
        name: name,
      };

      try {
        // Simulate an API POST request - replace with actual this.$http.post or Axios call
        const res = await fetch("/api/downloadDocuments", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(params),
        });

        const { base64Data } = await res.json();

        if (typeof base64Data !== "string" || !base64Data.match(/^[A-Za-z0-9+/=\s]+$/)) {
          throw new Error("Invalid base64 data received");
        }

        const binaryData = atob(base64Data);
        const arrayBuffer = new ArrayBuffer(binaryData.length);
        const byteArray = new Uint8Array(arrayBuffer);
        for (let i = 0; i < binaryData.length; i++) {
          byteArray[i] = binaryData.charCodeAt(i);
        }

        const blob = new Blob([byteArray], { type: "application/pdf" });
        const url = window.URL.createObjectURL(blob);
        const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);

        if (isSafari) {
          const newTab = window.open("about:blank");
          if (newTab) {
            newTab.location.href = url;
            setTimeout(() => URL.revokeObjectURL(url), 10000);
          } else {
            this.$notify?.({
              type: "error",
              message: "Popup blocked. Please allow popups or download manually.",
            }) || alert("Popup blocked. Please allow popups.");
            window.location.href = url;
          }
        } else {
          const a = document.createElement("a");
          a.href = url;
          a.download = name;
          document.body.appendChild(a);
          a.click();
          document.body.removeChild(a);
          setTimeout(() => URL.revokeObjectURL(url), 5000);
        }
      } catch (error) {
        console.error("Download failed", error);
        this.$notify?.({
          type: "error",
          message: "Failed to download document. Please try again.",
        }) || alert("Failed to download document. Please try again.");
      }
    },
  },
};
</script>

<style scoped>
.download-container {
  padding: 20px;
}
button {
  margin: 10px;
  padding: 10px 20px;
  background-color: #0099ff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #007acc;
}
</style>
