# 🌍 Language Detector

A high-performance C++ application that detects the language of input text using word frequency analysis and fuzzy matching with Levenshtein distance.

## ✨ Features

- **Multi-language Support**: Detect English, French, Hindi, and extensible to more languages
- **Intelligent Matching**: 
  - Exact word matching with frequency scoring
  - Fuzzy matching using Levenshtein distance for typos and variations
  - Weighted scoring system for accurate detection
- **Efficient Data Structure**: Uses hash maps for O(1) lookup performance
- **Robust Text Processing**: Automatic lowercase conversion and punctuation removal
- **Dictionary-Based Approach**: Leverages comprehensive word frequency dictionaries

## 🏗️ Architecture

### Core Components

1. **Word Tokenization** - Converts input text into cleaned tokens
2. **Dictionary Loading** - Loads language dictionaries from `.txt` files
3. **Scoring Engine** - Evaluates text against each language's word frequencies
4. **Language Detection** - Identifies the most likely language

### Algorithm Details

- **Exact Match Score**: `10 + word_frequency`
- **Fuzzy Match Score** (edit distance ≤ 2): `3 - distance`
- **Final Detection**: Language with highest cumulative score wins

## 📁 Project Structure

```
language-detector/
├── language_detector.cpp      # Main application source
├── english.txt                # English word frequency dictionary
├── french.txt                 # French word frequency dictionary
└── hindi.txt                  # Hindi word frequency dictionary
```

## 🚀 Getting Started

### Prerequisites

- C++17 or higher
- A C++ compiler (g++, clang, or MSVC)

### Build

```bash
cd language-detector
g++ -std=c++17 -o language_detector language_detector.cpp
```

Or with modern C++:
```bash
g++ -std=c++20 -O2 -o language_detector language_detector.cpp
```

### Run

```bash
./language_detector
```

**Example Usage:**
```
Loading language dictionaries...
Loaded 3 languages.
Enter a sentence: Hello, how are you today?

Detected Language: english
```

## 💡 How It Works

1. **Dictionary Loading** - Reads word-frequency pairs from dictionary files
2. **Input Processing** - Tokenizes user input, removes punctuation, converts to lowercase
3. **Scoring** - For each word:
   - Exact match → add `10 + frequency`
   - Close match (edit distance ≤ 2) → add `3 - distance`
4. **Detection** - Returns language with the highest total score

## 🔧 Customization

### Adding New Languages

1. Create a new file: `language_name.txt`
2. Format: Each line should contain `word frequency` (space-separated)
3. Example:
   ```
   bonjour 1250
   merci 980
   oui 1100
   ```
4. Place in the `dictionaries/` directory
5. Recompile and run!

### Adjusting Scoring

Modify these values in `language_detector.cpp`:

```cpp
scores[lang] += 10 + dict.at(word);  // Exact match boost (line 83)
scores[lang] += 3 - dist;             // Fuzzy match boost (line 90)
int bestDist = 3;                     // Fuzzy match threshold (line 86)
```

## 📊 Supported Languages

- 🇺🇸 English
- 🇫🇷 French
- 🇮🇳 Hindi

*Easily extensible to support more languages!*

## 🎯 Key Functions

| Function | Purpose |
|----------|---------|
| `tokenize()` | Converts input string to word vector |
| `toLower()` | Case normalization |
| `editDistance()` | Calculates Levenshtein distance |
| `loadDictionaries()` | Loads all language dictionaries |
| `detectLanguage()` | Performs language detection |

## ⚙️ Performance

- **Time Complexity**: O(n × m × k) where n = input words, m = dictionary size, k = average word length
- **Space Complexity**: O(d × w) where d = number of languages, w = total words in dictionaries
- **Optimization**: Hash maps provide O(1) average lookup

## 🐛 Known Limitations

- Short text snippets may have lower accuracy
- Requires trained dictionaries with word frequencies
- Edit distance calculation can be slow for very long words (mitigated with threshold)
- Single-word detection accuracy depends on dictionary comprehensiveness

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Add more language dictionaries
- Improve the scoring algorithm
- Optimize performance
- Fix bugs

## 📝 License

This project is open source and available under the MIT License.

## 👨‍💻 Author

**Praveen Penigadi**

---

**Made with ❤️ for language detection**
