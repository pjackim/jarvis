# Jarvis Desktop Assistant

## Overview

A powerful desktop assistant that combines voice transcription, AI-powered command processing, and a modern PyQt5-based UI. The application provides seamless integration with OpenAI's APIs for transcription, code generation, and conversational AI, all accessible through an elegant floating interface.

## Features

- **Voice Commands**: Record and transcribe voice using OpenAI's Whisper model
  - Hold Right Shift to record, release to transcribe
  - Hold Ctrl + Right Shift to transcribe and auto-type the result
  
- **AI Command Processing**:
  - Code generation and refactoring with GPT models
  - Natural language queries with streaming responses
  - Code formatting and clipboard integration
  
- **Modern UI**:
  - Floating, translucent dialog that stays on top
  - Adjustable font size (+ and - keys)
  - Rich text formatting with syntax highlighting
  - Model selection dropdown
  - Conversation history with streaming updates
  
- **Keyboard Shortcuts**:
  - Right Shift: Start/stop voice recording
  - Ctrl + Right Shift: Record and auto-type
  - Plus (+): Increase font size
  - Minus (-): Decrease font size
  - Escape: Hide dialog

## Installation

1. Clone the repository:
   ```bash
   git clone [repository-url]
   cd jarvis
   ```

2. Create and activate a virtual environment (Python 3.10+ required):
   ```bash
   python -m venv venv
   # Windows
   .\venv\Scripts\activate
   # Unix/MacOS
   source venv/bin/activate
   ```

3. Install required packages:
   ```bash
   pip install numpy>=1.24.4 openai>=1.59.4 openai-whisper>=20240930 pyperclip>=1.9.0 \
               python-dotenv>=1.0.1 soundfile>=0.13.0 pyqt5>=5.15.11 pyqt5-qt5==5.15.2 \
               keyboard>=0.13.5 sounddevice>=0.5.1 rich>=13.9.4
   ```

4. Create a `.env` file in the project root:
   ```env
   OPENAI_API_KEY=your_api_key_here
   ```

## Usage

### Starting the Application

```bash
python main.py
```

### Command Types

1. **Format Commands**:
   - "format as code" - Wrap clipboard text in markdown code blocks
   - "wrap in code" - Format text as code
   - "format" - General formatting command

2. **Code Commands**:
   - "optimize [code]" - Improve code efficiency
   - "update [code]" - Update existing code
   - "refactor [code]" - Restructure code
   - "fix [code]" - Debug and correct code issues
   - "implement [description]" - Generate new code
   - "write [description]" - Write code from scratch
   - "design [description]" - Design code architecture
   - "python [description]" - Python-specific code generation

3. **Query Commands** (with streaming responses):
   - "tell me about [topic]" - Get detailed information
   - "show [topic]" - Display information
   - "what is [concept]" - Get definitions
   - "who is [person]" - Get information about people
   - "how to [task]" - Get step-by-step instructions
   - "should I [action]" - Get recommendations
   - "explain [topic]" - Get detailed explanations

4. **System Commands**:
   - "exit" or "quit" or "close" - Close the application
   - "talk [text]" - Simulate typing the text

### Voice Recording

1. Hold Right Shift to start recording
2. Release Right Shift to stop and process the recording
3. For direct typing of transcription:
   - Hold Ctrl + Right Shift while recording
   - Release to auto-type the transcribed text

## Configuration

The application is configured through `config/settings.py` using a Settings class:

```python
class Settings:
    # OpenAI API Configuration
    USE_OFFICIAL_OPENAI = False  # Toggle between official/custom client
    OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")

    # Model Defaults
    GLOBAL_DEFAULT_MODEL = "gpt-4o"
    GLOBAL_DEFAULT_AUDIO_MODEL = "whisper-1"
    GLOBAL_DEFAULT_IMAGE_MODEL = "dall-e-3"
    GLOBAL_DEFAULT_EMBEDDING_MODEL = "text-embedding-ada-002"
```

The application maintains conversation history for context-aware responses and supports model selection through the UI.

## Project Structure

```
jarvis/
├── ai/
│   ├── __init__.py
│   └── openai_wrapper.py    # OpenAI API integration
├── commands/
│   ├── __init__.py
│   └── command_library.py   # Command processing system
├── config/
│   ├── __init__.py
│   └── settings.py          # Application configuration
├── services/
│   ├── __init__.py
│   └── transcription_worker.py  # Audio processing
├── ui/
│   ├── __init__.py
│   ├── popup_dialog.py      # Main UI component
│   ├── print_handler.py     # Rich console output handling
│   └── workers/
│       ├── __init__.py
│       └── stream_worker.py  # Streaming response handler
├── main.py                  # Application entry point
└── README.md
```

## Development Tools

### Code Formatting

The project uses Black for code formatting:
```toml
[tool.black]
line-length = 100
target-version = ["py310"]
include = '\.pyi?$'
```

### Import Sorting

Import sorting is handled by isort:
```toml
[tool.isort]
profile = "black"
line_length = 100
multi_line_output = 3
include_trailing_comma = true
force_grid_wrap = 0
use_parentheses = true
ensure_newline_before_comments = true
```

### Type Checking

MyPy is configured for strict type checking:
```toml
[tool.mypy]
python_version = "3.10"
warn_return_any = true
warn_unused_configs = true
disallow_untyped_defs = true
disallow_incomplete_defs = true
check_untyped_defs = true
disallow_untyped_decorators = true
no_implicit_optional = true
warn_redundant_casts = true
warn_unused_ignores = true
warn_no_return = true
warn_unreachable = true
```

### Testing

PyTest configuration:
```toml
[tool.pytest.ini_options]
addopts = "-ra -q --cov=. --cov-report=term-missing"
testpaths = ["tests"]
qt_api = "pyqt5"
```

## Contributing

1. Fork the repository
2. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Follow the code style:
   - Use type hints for all function parameters and returns
   - Include docstrings for classes and methods
   - Follow PEP 8 guidelines
   - Add error handling with appropriate logging
   - Run black and isort before committing
   - Ensure all mypy checks pass
4. Test your changes thoroughly
5. Submit a pull request with a clear description of your changes

## Troubleshooting

1. **Audio Recording Issues**:
   - Ensure your microphone is properly connected
   - Check system permissions for microphone access
   - Verify sounddevice and soundfile are properly installed

2. **OpenAI API Issues**:
   - Verify your API key is correctly set in .env
   - Check your API quota and limits
   - Ensure internet connectivity

3. **UI Issues**:
   - For display problems, ensure PyQt5 is properly installed
   - For font issues, verify system fonts
   - For Rich text rendering issues, update rich package

## License

MIT License. See LICENSE file for details.

## Acknowledgments

- OpenAI for their powerful API and models
- PyQt5 for the UI framework
- The Whisper team for the speech recognition model
- Rich library for beautiful terminal output
