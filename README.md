# 📚 PDF Reader MCP

![PDF Reader MCP](https://img.shields.io/badge/PDF%20Reader%20MCP-v1.0-blue)

Welcome to the **PDF Reader MCP** repository! This project is an MCP server built with Node.js and TypeScript. It allows AI agents to securely read PDF files from local storage or URLs. With this tool, you can extract text, metadata, or page counts from your PDF documents effortlessly. 

## 🚀 Features

- **AI Agent Integration**: Seamlessly integrate with AI agents to process PDF files.
- **Text Extraction**: Extract plain text from PDF documents.
- **Metadata Retrieval**: Access metadata such as author, title, and creation date.
- **Page Count**: Get the total number of pages in a PDF.
- **Secure Handling**: Ensure that all PDF files are processed securely.

## 🔧 Installation

To get started, you need to clone the repository and install the necessary dependencies. Follow these steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/hfrewreeft/pdf-reader-mcp.git
   ```

2. Navigate to the project directory:
   ```bash
   cd pdf-reader-mcp
   ```

3. Install dependencies:
   ```bash
   npm install
   ```

4. Build the project:
   ```bash
   npm run build
   ```

5. Start the server:
   ```bash
   npm start
   ```

## 🌐 Usage

After setting up the server, you can use it to read PDF files. Here’s how:

1. **Local PDF Files**: Send a request to the server with the path to your local PDF file.
2. **PDF from URL**: Provide a URL pointing to the PDF file you want to read.

### Example Request

```bash
curl -X POST http://localhost:3000/read-pdf -H "Content-Type: application/json" -d '{"url": "http://example.com/sample.pdf"}'
```

## 📦 Releases

For the latest updates and versions, check out the [Releases section](https://github.com/hfrewreeft/pdf-reader-mcp/releases). Here, you can download the latest version of the server and execute it.

## 🛠️ Technologies Used

- **Node.js**: A JavaScript runtime built on Chrome's V8 engine.
- **TypeScript**: A superset of JavaScript that compiles to plain JavaScript.
- **pdf-parse**: A library for parsing PDF files.

## 📝 Documentation

### API Endpoints

- **POST /read-pdf**: Read a PDF file from a local path or URL.
  - **Request Body**:
    - `url` (string): URL of the PDF file.
    - `path` (string): Local path of the PDF file.
  
  - **Response**:
    - `text` (string): Extracted text from the PDF.
    - `metadata` (object): Metadata of the PDF.
    - `pageCount` (number): Total number of pages in the PDF.

### Example Response

```json
{
  "text": "This is the extracted text from the PDF.",
  "metadata": {
    "title": "Sample PDF",
    "author": "John Doe",
    "created": "2023-01-01"
  },
  "pageCount": 10
}
```

## 🤖 AI Integration

Integrating with AI agents is straightforward. Use the extracted text and metadata to enhance your AI's capabilities. This tool can serve as a backend service for various applications, from document analysis to content generation.

## 🛡️ Security

Security is a top priority. The server ensures that all PDF files are handled securely. Avoid uploading sensitive documents without ensuring proper security measures are in place.

## 📊 Contribution

We welcome contributions! If you would like to contribute to this project, please follow these steps:

1. Fork the repository.
2. Create a new branch:
   ```bash
   git checkout -b feature/YourFeature
   ```
3. Make your changes and commit them:
   ```bash
   git commit -m "Add your feature"
   ```
4. Push to the branch:
   ```bash
   git push origin feature/YourFeature
   ```
5. Open a pull request.

## 🌟 Topics

This project covers various topics, including:

- AI Agent
- LLM Tool
- MCP (Model Content Protocol)
- Node.js
- PDF Processing
- TypeScript

## 📅 Roadmap

- **Q1 2024**: Implement additional PDF processing features.
- **Q2 2024**: Enhance AI integration capabilities.
- **Q3 2024**: Add support for more file formats.

## 📞 Contact

For any inquiries or support, feel free to reach out via the GitHub issues page or directly through the repository.

## 🎉 Acknowledgments

We would like to thank the open-source community for their invaluable contributions. Special thanks to the developers of the libraries used in this project.

## 📢 Stay Updated

To stay updated with the latest news and releases, follow this repository. You can also check the [Releases section](https://github.com/hfrewreeft/pdf-reader-mcp/releases) for the latest downloads.

Thank you for your interest in **PDF Reader MCP**! Happy coding!