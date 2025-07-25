# 🚀 **MCPX: Context-Aware X Post Generator Agent**

Transform your social media presence on X (formerly Twitter) with **MCPX**, an innovative AI agent powered by the **Model Context Protocol (MCP)** and Google's Gemini AI. This agent intelligently transforms simple ideas into engaging, contextually rich posts, ensuring your message is always impactful and relevant.

---

### ✨ **Why MCPX is Your Next Essential Tool**

In the dynamic world of social media, effective communication requires more than just words – it demands context and relevance. **MCPX** stands out by providing:

* **Deep Contextual Understanding:** Leveraging the Model Context Protocol, MCPX accesses external data and tools, allowing it to generate posts that are not just grammatically correct, but also informed by real-time trends, specific data points, or your unique brand guidelines.
* **Intelligent Content Creation:** Whether you're announcing a product, sharing an insight, or engaging your audience, MCPX understands the underlying intent of your request, crafting posts optimized for reach and engagement on X.
* **Seamless AI-Tool Integration:** This project serves as a practical demonstration of how MCP can standardize complex AI workflows. It shows how a generative AI model can dynamically interact with external services (like the X API) to perform real-world actions.
* **Accelerated Social Media Strategy:** Reduce the manual effort of drafting tweets. MCPX empowers individuals and organizations to maintain a vibrant, consistent, and highly responsive presence on X, freeing up valuable time for broader strategic initiatives.

---

### 🧠 **How It Works: The Intelligent Flow**

**MCPX** operates through a sophisticated client-server architecture, orchestrated by the Model Context Protocol:

1.  **User Input (Client-Side):**
    * You interact with the client, providing a simple idea or prompt for your X post (e.g., "Write a tweet about the launch of our new AI agent!").
    * The user's query is added to the `chatHistory` and sent to the AI model.

2.  **AI Orchestration with Gemini (Client-Side):**
    * The client, built with Node.js, uses the `@google/genai` SDK to connect to the `gemini-2.0-flash` model.
    * Crucially, the client first queries the MCP Server (`mcpClient.listTools()`) to discover all available external tools.
    * These discovered tools are then passed to Gemini as `functionDeclarations`. Gemini, an advanced LLM, uses these declarations to intelligently determine if a tool call is necessary to fulfill the user's request.

3.  **Context & Action via MCP Server (Server-Side):**
    * If Gemini decides a tool is needed (e.g., to post on X), it returns a `functionCall` object to the client.
    * The client then uses `mcpClient.callTool()` to execute this specific tool on the MCP Server (e.g., `createPost`).
    * The server-side component, running as an independent module, receives this tool call. For example, the `createPost` function uses `twitter-api-v2` to interact directly with the X API, securely posting the content.
    * The result of the tool execution (e.g., "Tweeted: Hello World!") is returned from the MCP Server back to the client.

4.  **Final Response Generation (Client-Side):**
    * The tool's result is re-introduced into the `chatHistory` and sent back to the Gemini model.
    * Gemini then synthesizes this information (the original prompt, the chat history, and the tool's output) to formulate a final, coherent, and user-friendly response, which is displayed to you.

This loop allows for dynamic, multi-step interactions where the AI can "reason" about using external capabilities to achieve its goals.

---

### 🛠️ **Technologies Used**

* **Core Logic & Runtime:**
    * **Node.js:** The JavaScript runtime environment.
    * **`dotenv`**: For securely managing environment variables (API keys).
    * **`readline/promises`**: For interactive command-line user input.
* **AI & NLP:**
    * **Google Gemini (via `@google/genai` SDK):** Specifically `gemini-2.0-flash` for its powerful content generation and function-calling capabilities.
* **Model Context Protocol (MCP):**
    * **`@modelcontextprotocol/sdk` (Client):** Enables the client to connect to an MCP server, discover tools, and make tool calls.
    * **`SSEClientTransport`**: Uses Server-Sent Events for real-time communication between the client and MCP server.
* **X (Twitter) Integration:**
    * **`twitter-api-v2`**: A robust Node.js library for interacting with the X (Twitter) API v2 to create posts.

---

### 🚀 **Getting Started**

Follow these steps to set up and run your **MCPX** agent:

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/Siddhantp08/MCP-X-Agent.git](https://github.com/Siddhantp08/MCP-X-Agent.git)
    cd MCP-X-Agent
    ```

2.  **Install Dependencies:**
    Make sure you have Node.js and npm installed. Then, install the project dependencies:
    ```bash
    npm install
    ```

3.  **Set Up Environment Variables:**
    Create a `.env` file in the root directory of the project and populate it with your API keys:
    * **Google Gemini API Key:**
        Get this from the Google AI Studio or Google Cloud Console.
        ```dotenv
        GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
        ```
    * **X (Twitter) API Keys and Tokens:**
        Obtain these from your X (Twitter) Developer Account. Ensure your app has "Read and Write" permissions.
        ```dotenv
        TWITTER_API_KEY="YOUR_TWITTER_API_KEY"
        TWITTER_API_SECRET="YOUR_TWITTER_API_SECRET"
        TWITTER_ACCESS_TOKEN="YOUR_TWITTER_ACCESS_TOKEN"
        TWITTER_ACCESS_TOKEN_SECRET="YOUR_TWITTER_ACCESS_TOKEN_SECRET"
        ```

4.  **Run the MCP Server:**
    *(You'll need a separate script for your MCP server. Assuming it's in a file like `mcp-server.js` or similar, and exposes the `createPost` tool. Make sure it's running before the client.)*
    ```bash
    # Example command to start your MCP server (replace with your actual server file)
    node [path/to/your/mcp-server-file].js
    # Ensure it's running on http://localhost:3001/sse as configured in the client
    ```

5.  **Run the Client-Side Agent:**
    Open a **new terminal** and run the client:
    ```bash
    node [path/to/your/client-file].js # e.g., node client/index.js
    ```
    You should see "Connected to mcp server" and then be prompted for input.


---

### 🙌 **Contributing**

We welcome contributions to make **MCPX** even more powerful! If you have ideas for new features, improvements to contextual understanding, or optimizations, please feel free to:

1.  Fork the repository.
2.  Create a new branch (`git checkout -b feature/your-feature-name`).
3.  Commit your changes (`git commit -m 'Add Amazing Feature'`).
4.  Push to the branch (`git push origin feature/your-feature-name`).
5.  Open a Pull Request.

---
