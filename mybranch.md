```
npm run dev
```



```
// client.js
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import path from "path";
import {fileURLToPath} from 'url';

import { SSEClientTransport } from "@modelcontextprotocol/sdk/client/sse.js";

async function runClient() {
    const client = new Client(
        {
            name: "mcp-typescript test client",
            version: "0.1.0",
        },
    );


    const clientTransport = new SSEClientTransport(new URL("http://localhost:3333/sse"));

    await client.connect(clientTransport);
    const tools = await client.listTools()
    console.log(tools)
    const resp0 = await client.callTool({
        name: "hello_world",
        arguments: {
            yourName: "lala"
        }
    })

    console.log(resp0);


    const resp1 = await client.callTool({
        name: "get_figma_data",
        arguments: {
            fileKey: "SRYkCs9QjXTFKMj9oM831s",
            nodeId: "16-59"
        }
    })
    console.log(resp1);

    debugger
    const __filename = fileURLToPath(import.meta.url);
    const __dirname = path.dirname(__filename);

    const resp2 = await client.callTool({
        name: "download_figma_images",
        arguments: {
            fileKey: "SRYkCs9QjXTFKMj9oM831s",
            nodes: [
                {
                    // nodeId: '16:80',
                    // nodeId: '16:72',
                    nodeId: '16:105',
                    imageRef: "",
                    fileName: "a.svg"
                }
            ],
            localPath: path.join(__dirname, 'cache')
        }
    })
    console.log(resp2);
    debugger
    await client.close();
}

runClient();
```


调试
chrome://inspect/#devices



mcp client
https://zhuanlan.zhihu.com/p/1889258896595611956

https://github.com/modelcontextprotocol/typescript-sdk/issues/264

