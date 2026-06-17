# Text Tools

This is a project that uses Svelte as a front end framework, alongside Tailwind for CSS.

## Installing Node / NPM (if not already installed)

### Download and install nvm:
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.5/install.sh | bash
```

### in lieu of restarting the shell
```
\. "$HOME/.nvm/nvm.sh"
```

### Download and install Node.js:
```
nvm install 26
```

### Verify the Node.js version:
```
node -v # Should print "v26.3.0".
```

### Verify npm version:
```
npm -v # Should print "11.16.0".
```

## Developing

install dependencies with `npm install`

Then, start the server:

```sh
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```