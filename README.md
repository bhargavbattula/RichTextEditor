# RichEditor

A full-featured, free, and open-source WYSIWYG rich text editor built with vanilla JavaScript. No dependencies required.

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## Features

### Core Editing
- **Rich Text Formatting** - Bold, italic, underline, strikethrough, subscript, superscript
- **Font Controls** - 15+ font families (Arial, Georgia, Times New Roman, etc.)
- **Font Sizes** - 7 sizes from 8pt to 36pt
- **Line Height** - Adjustable line spacing (1.0 to 3.0)
- **Text & Background Colors** - Full color picker support

### Structure & Layout
- **Lists** - Ordered and unordered lists
- **Text Alignment** - Left, center, right, justify
- **Indentation** - Increase/decrease indent
- **Block Quotes** - Quote formatting
- **Horizontal Rules** - Section dividers

### Tables
- **Table Creation** - Visual grid selector for easy table insertion
- **Row/Column Management** - Add/delete rows and columns
- **Cell Formatting** - Text alignment, colors, and styles within cells
- **Table Properties** - Border, width, and cell padding controls

### Media & Links
- **Image Support** - Insert images via URL or file upload
- **Video Embedding** - YouTube, Vimeo, and direct video URLs
- **Hyperlinks** - Create and edit links with target options

### Code
- **Code Blocks** - Syntax-highlighted code sections
- **Inline Code** - Inline code formatting
- **Source View** - Edit raw HTML directly

### User Interface
- **Professional Menu Bar** - Edit, Insert, Format, and Table menus
- **Customizable Toolbar** - Show/hide buttons, reorder groups
- **Fullscreen Mode** - Distraction-free editing
- **Status Bar** - Word count, character count, HTML character count

### Advanced Features
- **Undo/Redo** - Full history support (Ctrl+Z / Ctrl+Y)
- **Keyboard Shortcuts** - Standard formatting shortcuts
- **Print Support** - Print editor content
- **Auto-Save** - Automatic content saving
- **RTL Support** - Right-to-left text direction
- **Plugin Architecture** - Extend with custom plugins

## Installation

### Via CDN
```html
<script src="https://unpkg.com/richeditor@1.0.0/richeditor.js"></script>
```

### Via npm
```bash
npm install richeditor
```

### Direct Download
Download `richeditor.js` and include it in your project:
```html
<script src="path/to/richeditor.js"></script>
```

## Quick Start

```html
<!DOCTYPE html>
<html>
<head>
    <title>RichEditor Demo</title>
</head>
<body>
    <textarea id="editor"></textarea>
    
    <script src="richeditor.js"></script>
    <script>
        const editor = new RichEditor('#editor', {
            height: 400,
            showMenuBar: true
        });
    </script>
</body>
</html>
```

## Configuration Options

```javascript
const editor = new RichEditor('#editor', {
    // Dimensions
    width: '100%',
    height: 400,
    minHeight: 200,
    maxHeight: 800,
    
    // UI Options
    showMenuBar: true,
    showToolbar: true,
    showStatusBar: true,
    theme: 'light',  // 'light' or 'dark'
    
    // Default Styles
    defaultFontFamily: 'Arial, sans-serif',
    defaultFontSize: '14pt',
    defaultLineHeight: '1.5',
    
    // Features
    enforceInlineStyles: true,  // Apply styles inline for email compatibility
    
    // Toolbar Groups
    toolbarGroups: [
        ['undo', 'redo'],
        ['formatBlock', 'fontFamily', 'fontSize'],
        ['bold', 'italic', 'underline', 'strikethrough'],
        ['foreColor', 'backColor'],
        ['alignLeft', 'alignCenter', 'alignRight', 'alignJustify'],
        ['orderedList', 'unorderedList'],
        ['link', 'image', 'video', 'table'],
        ['code', 'codeBlock', 'blockquote'],
        ['removeFormat', 'source', 'fullscreen']
    ],
    
    // Plugins
    plugins: [],
    
    // Callbacks
    onChange: (content) => { },
    onFocus: () => { },
    onBlur: () => { }
});
```

## API Methods

### Content Management
```javascript
// Get content
editor.getContent();         // Returns HTML
editor.getText();            // Returns plain text (normalized)
editor.getRawText();         // Returns raw innerText

// Set content
editor.setContent('<p>Hello World</p>');
editor.insertContent('<strong>Bold text</strong>');

// Clear content
editor.clear();

// Check if empty
editor.isEmpty();
```

### Statistics
```javascript
editor.getWordCount();       // Number of words
editor.getCharCount();       // Number of characters (normalized)
editor.getHtmlCharCount();   // Number of HTML characters
```

### Editor Control
```javascript
editor.focus();
editor.enable();
editor.disable();
editor.destroy();
```

### Commands
```javascript
// Execute formatting command
editor.execCommand('bold');
editor.execCommand('fontName', 'Georgia');
editor.execCommand('fontSize', '18pt');
editor.execCommand('foreColor', '#ff0000');
```

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Ctrl + B | Bold |
| Ctrl + I | Italic |
| Ctrl + U | Underline |
| Ctrl + Z | Undo |
| Ctrl + Y | Redo |
| Ctrl + Shift + Z | Redo |
| Ctrl + A | Select All |
| Ctrl + P | Print |

## Plugins

### Built-in Plugins

```javascript
// Word Count Enhanced Plugin
const editor = new RichEditor('#editor', {
    plugins: [RichEditorPlugins.WordCount]
});

// Emoji Plugin
const editor = new RichEditor('#editor', {
    plugins: [RichEditorPlugins.Emoji]
});

// Find & Replace Plugin
const editor = new RichEditor('#editor', {
    plugins: [RichEditorPlugins.FindReplace]
});
```

### Creating Custom Plugins

```javascript
class MyPlugin extends RichEditorPlugin {
    constructor(editor) {
        super(editor);
        this.name = 'myPlugin';
    }
    
    init() {
        // Add toolbar button
        this.editor.addToolbarButton('myButton', {
            icon: 'custom',
            title: 'My Button',
            action: 'myAction'
        });
        
        // Handle action
        const originalExecAction = this.editor.execAction.bind(this.editor);
        this.editor.execAction = (action, value) => {
            if (action === 'myAction') {
                // Custom logic
            } else {
                originalExecAction(action, value);
            }
        };
    }
}

// Register plugin
const editor = new RichEditor('#editor', {
    plugins: [MyPlugin]
});
```

## Browser Support

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Author

**Bhargav Battula**

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Changelog

### Version 1.0.0
- Initial release
- Full-featured WYSIWYG editing
- Professional menu bar
- Table support with cell formatting
- Plugin architecture
- Keyboard shortcuts
- Multiple themes
