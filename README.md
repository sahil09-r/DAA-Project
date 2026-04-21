# Huffman Compressor

A **File Compression Tool** built from scratch using Huffman Coding.  
This is a classic DSA project demonstrating real compression with hand-coded data structures.

## Data Structures Used

| Structure | File | Role |
|-----------|------|------|
| Min Heap / Priority Queue | `src/utils/MinHeap.js` | Extracts lowest-frequency nodes during tree construction |
| Binary Tree | `src/utils/HuffmanNode.js` | Stores the Huffman encoding tree (left=0, right=1) |
| HashMap / Dictionary | `src/utils/huffman.js` | Maps char → binary code for O(1) encoding lookup |
| Frequency Table | `src/utils/huffman.js` | O(n) first pass to count character occurrences |

## Features

- **Compress** `.txt` files — paste text, type, or drag & drop a file
- **Save** the compressed output as a `.huff` file (JSON with bit string + code table)
- **Decompress** `.huff` files — drag & drop or use last result — recovers original text exactly
- **Tree View** — live canvas rendering of the Huffman binary tree + algorithm walkthrough

## Project Structure

```
huffman-compressor/
├── index.html
├── vite.config.js
├── package.json
├── src/
│   ├── main.jsx              # React entry point
│   ├── App.jsx               # Root component + tab routing
│   ├── styles.css            # Global styles
│   ├── utils/
│   │   ├── MinHeap.js        # Min Heap (Priority Queue) — DSA core
│   │   ├── HuffmanNode.js    # Binary Tree node
│   │   └── huffman.js        # Full algorithm: compress, decompress, encode, decode
│   └── components/
│       ├── CompressTab.jsx   # UI for compression
│       ├── DecompressTab.jsx # UI for decompression
│       ├── TreeTab.jsx       # Tree visualization + DS info
│       └── TreeCanvas.jsx    # HTML5 Canvas tree renderer
```

## Getting Started

```bash
# 1. Install dependencies
npm install

# 2. Start dev server
npm run dev

# 3. Open in browser
# → http://localhost:5173
```

## How Huffman Coding Works

1. **Count frequencies** — scan the entire input, count how often each character appears
2. **Build Min Heap** — insert all characters as leaf nodes, sorted by frequency
3. **Build tree** — repeatedly pop two lowest nodes, merge them into a parent, push back
4. **Generate codes** — DFS the tree (left=0, right=1), collect path for each leaf
5. **Encode** — replace each character with its code from the HashMap
6. **Decode** — traverse the tree bit-by-bit; emit character at each leaf node

## Complexity

| Operation | Time | Space |
|-----------|------|-------|
| Build frequency map | O(n) | O(k) |
| Build heap | O(k log k) | O(k) |
| Generate codes | O(k) | O(k) |
| Encode | O(n) | O(n) |
| Decode | O(m) | O(k) |

Where `n` = input length, `k` = unique characters, `m` = compressed bit length.
