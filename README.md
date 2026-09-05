# GS1 Barcode & Digital Link Decoder — TypeScript / JavaScript SDK

[![npm version](https://img.shields.io/npm/v/@stanzaapi/gs1-decoder.svg)](https://www.npmjs.com/package/@stanzaapi/gs1-decoder)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Stanza API](https://img.shields.io/badge/Powered%20by-Stanza-blue)](https://stanzaapi.com)

> Decode GS1 DataMatrix, GS1-128, FNC1 barcodes, and GS1 Digital Link URIs into structured JSON in sub-5ms.

Official, zero-dependency Node.js and TypeScript client for **GS1 Barcode & Digital Link Decoder**, powered by the [Stanza Micro-API Network](https://stanzaapi.com). Delivers deterministic, sub-5ms V8 isolate execution directly to your application without 3rd-party proxies.

* 🌐 **Live Web Sandbox:** [Try interactive queries online](https://stanzaapi.com/tools/gs1-decoder)
* 📚 **API Reference:** [Read complete OpenAPI specification](https://stanzaapi.com/tools/gs1-decoder)
* ⚡ **Platform Overview:** [Discover the Stanza Edge Portfolio](https://stanzaapi.com)

---

## 📦 Installation

```bash
npm install @stanzaapi/gs1-decoder
# or
pnpm add @stanzaapi/gs1-decoder
# or
yarn add @stanzaapi/gs1-decoder
```

---

## 🚀 Quickstart

```typescript
import { Gs1DecoderClient } from '@stanzaapi/gs1-decoder';

// Initialize client (API key optional for sandbox tier evaluation)
const client = new Gs1DecoderClient({
  apiKey: process.env.STANZA_API_KEY,
});

async function main() {
  const result = await client.parse('(01)00123456789012(21)12345');

  if (result.success) {
    console.log('Verification Success:', result.data);
  } else {
    console.error('Validation Error:', result.error, result.code);
  }
}

main().catch(console.error);
```

---

## 📄 Example JSON Response

```json
{
  "success": true,
  "data": {
    "gtin": "00123456789012",
    "serial_number": "12345",
    "ai_elements": [
      {
        "ai": "01",
        "label": "GTIN",
        "value": "00123456789012"
      },
      {
        "ai": "21",
        "label": "SERIAL",
        "value": "12345"
      }
    ]
  }
}
```

---

## ⚙️ Client Configuration Options

| Option | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `apiKey` | `string` | `process.env.STANZA_API_KEY` | Your [Stanza API Key](https://stanzaapi.com). Required for high-throughput production tiers. |
| `baseUrl` | `string` | `https://stanzaapi.com` | Edge API endpoint base URL. Configurable for private enterprise enclaves. |
| `timeoutMs` | `number` | `15000` | Request timeout in milliseconds (uses native `AbortSignal.timeout`). |


---

## 🛡️ Response Envelope & Error Handling

All responses return a typed envelope:

```typescript
export interface ApiResponse<T> {
  success: boolean;
  data?: T;
  error?: string;
  code?: 'VALIDATION_ERROR' | 'UNAUTHORIZED' | 'PAYLOAD_TOO_LARGE' | 'RATE_LIMITED' | 'INTERNAL_ERROR';
}
```

---

## 🔗 Related Resources

* [GS1 Barcode & Digital Link Decoder Interactive Playground](https://stanzaapi.com/tools/gs1-decoder)
* [Stanza Microservices Directory](https://stanzaapi.com)
* [Report an Issue on GitHub](https://github.com/stanzaapi/gs1-decoder-typescript/issues)

## 📄 License

MIT © Stanza — Powered by [Stanza](https://stanzaapi.com).
