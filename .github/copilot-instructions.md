# Abracadabra Educational Web Development Project

**ALWAYS follow these instructions exactly and only search for additional information if these instructions are incomplete or found to be in error.**

This is an educational npm workflow project that teaches students professional web development automation by transforming a corporate website into a magical cowsay-powered experience. The project demonstrates npm scripts, development servers, and environment-aware JavaScript transformations.

## Working Effectively

### Bootstrap the Project
Follow these exact commands in sequence:

```bash
# Initialize npm (creates package.json)
npm init -y

# Install required development dependencies - NEVER CANCEL: Takes ~8 seconds
npm install --save-dev cowsay http-server

# Add the required npm scripts to package.json (see Scripts section below)
```

**CRITICAL**: You MUST add the exact scripts shown in the Scripts section to package.json or the magic transformation will not work.

### Scripts Required in package.json
Add these EXACT scripts to your package.json (replace the default "test" script):

```json
{
  "scripts": {
    "generate": "cowsay 'Welcome to the most AWESOME website ever!' > generated/welcome.txt && cowsay -f dragon 'I am the guardian of this amazing site!' > generated/dragon.txt && cowsay -f tux 'Professional development tools make everything better!' > generated/tux.txt && node scripts/build-content.js",
    "serve": "http-server -p 3000 -o",
    "dev": "npm run generate && npm run serve"
  }
}
```

### Development Workflow Commands

#### Generate Content
```bash
npm run generate
```
- **Time**: ~0.4 seconds - very fast
- **Purpose**: Creates cowsay ASCII art files and builds HTML content
- **Output**: Creates `welcome.txt`, `dragon.txt`, `tux.txt`, and `cowsay-content.html` in generated/ directory
- **Error handling**: Will fail with "cowsay: not found" if cowsay is not installed

#### Start Development Server
```bash
npm run serve
```
- **Time**: Starts immediately, runs indefinitely until stopped with Ctrl+C
- **Purpose**: Starts http-server on port 3000 and opens browser
- **Critical**: The magic transformation ONLY works on port 3000 - other ports show guidance messages
- **Error handling**: Will fail with "http-server: not found" if http-server is not installed

#### Complete Development Workflow
```bash
npm run dev
```
- **Time**: ~0.4 seconds for generate, then starts server indefinitely
- **Purpose**: Runs generate then serve in sequence
- **NEVER CANCEL**: This is the primary command for the full experience

## Validation

### Manual Testing Requirements
**ALWAYS test the complete user scenario after making any changes:**

1. **Run the complete workflow**: `npm run dev`
2. **Verify server starts**: Should open http://127.0.0.1:3000 automatically
3. **Verify transformation occurs**: Page should transform from boring ACME Corporation to "Abracadabra Magic! 🪄" with cowsay ASCII art
4. **Test the magic countdown**: Wait for 3-second delay and 5-second countdown before transformation
5. **Verify title change**: Browser title should change from "ACME Corporation - Professional Business Solutions" to "Abracadabra Magic! 🪄"

### Specific Test Scenarios
- **Generated files exist**: Check that `generated/welcome.txt`, `generated/dragon.txt`, `generated/tux.txt`, and `generated/cowsay-content.html` are created
- **Port 3000 requirement**: The transformation only works when served on port 3000 via npm scripts
- **Error modes**: Test behavior when cowsay or http-server packages are missing

## Common Tasks

### Verify Installation
```bash
# Check installed packages
npm list --depth=0

# Should show:
# ├── cowsay@1.6.0
# └── http-server@14.1.1
```

### Clean Generated Files
```bash
# Remove all generated content (for testing)
rm -rf generated/*.txt generated/*.html
```

### Troubleshooting Commands
```bash
# If cowsay is missing
npm install --save-dev cowsay

# If http-server is missing  
npm install --save-dev http-server

# If packages are corrupted
rm -rf node_modules package-lock.json
npm install
```

## Project Structure Reference

### Repository Root
```
.
├── README.md              # Comprehensive project documentation
├── index.html             # Main HTML file with transformation logic
├── package.json           # NPM configuration (created by npm init)
├── .github/               # GitHub workflows and issue templates
├── .vscode/               # VS Code settings for Live Server
├── css/                   # Stylesheets for both modes
│   └── styles.css
├── js/                    # JavaScript transformation logic
│   └── magic.js
├── scripts/               # Build scripts
│   └── build-content.js
├── generated/             # Generated cowsay content (created by npm scripts)
│   ├── .gitkeep
│   └── [generated files]
├── docs/                  # Documentation and examples
└── node_modules/          # NPM dependencies (created by npm install)
```

### Key Files
- **index.html**: Contains the transformation HTML and includes magic.js
- **js/magic.js**: Port detection and transformation logic (394 lines)
- **scripts/build-content.js**: Combines cowsay files into HTML content (108 lines)
- **css/styles.css**: Two-mode theme styling (boring ACME + farm-themed awesome mode)

## Error Conditions and Solutions

### "cowsay: not found"
```bash
npm install --save-dev cowsay
```

### "http-server: not found"  
```bash
npm install --save-dev http-server
```

### "No such file or directory: generated/"
The generated directory exists with .gitkeep - this error shouldn't occur, but if it does:
```bash
mkdir -p generated
```

### Server won't start on port 3000
- Check if port 3000 is already in use
- Kill existing processes: `pkill -f "http-server"`
- Try the command again

### Page shows guidance messages instead of transformation
- **File:// protocol**: Shows "😴 Something's missing..." - Use npm run serve instead
- **Live Server (5500/5501)**: Shows "🤔 Close, but not quite right..." - Use npm run serve instead  
- **Other ports**: Shows port-specific guidance - Use npm run serve to get port 3000
- **Port 3000 without content**: Shows "⚡ Almost there!" - Run npm run generate first

## Development Notes

### No Linting/Formatting Tools
This project has no ESLint, Prettier, or other code quality tools configured. It's intentionally simple for educational purposes.

### No Build Process Beyond npm Scripts
The only "build" process is the npm scripts that generate cowsay content. There's no webpack, vite, or other bundler.

### Browser Compatibility
The project uses modern JavaScript (ES2015+) and requires a development server (not file://) for the transformation to work.

### Dependencies
- **cowsay@1.6.0**: Generates ASCII art animals with messages
- **http-server@14.1.1**: Simple HTTP server for development

## Success Criteria
- ✅ `npm init -y` creates package.json
- ✅ `npm install --save-dev cowsay http-server` completes in ~8 seconds
- ✅ package.json contains all required scripts exactly as specified
- ✅ `npm run generate` creates all expected files in ~0.4 seconds
- ✅ `npm run serve` starts server on port 3000 immediately
- ✅ Browser transformation: ACME → "Abracadabra Magic! 🪄" with cowsay ASCII art
- ✅ Complete workflow `npm run dev` executes successfully

This educational project demonstrates the power of npm scripts, development servers, and automated content generation in modern web development workflows.