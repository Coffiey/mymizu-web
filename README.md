# My Mizu Hackathon

pre-requisites:
- [NodeJS](https://nodejs.org/en/download/package-manager/)
- [Yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)

## Development

**Running the project locally**

All commands should be run in the project root directory.
```bash
# Create an .env file & insert the appropriate values
cp .env.sample .env

# Install dependencies
yarn 

# Compile both backend & client code
# Make sure to re-run this if you want to see your changes built
yarn build

# Compile for prod. This minifies the compiled files for production
yarn build:prod

# Run server with watch. This command will restart the server when a change has been detected
yarn start:reload

# Run server without watch
yarn start
```

**Routing / Adding Pages**

You can add routes to `server/server.jsx`, and be sure to import the component in which you'd like to inject into the html page, like so:

```javascript
import { YourCustomComponent } from "path/to/your/component"
//...
app.get("/a-new-page", (req, res) => {
  fs.readFile(path.resolve("./public/path/to/your/html/file.html"), "utf8", (err, data) => {
    if (err) {
      console.error(err);
      return res.status(500).send("An error occurred");
    }

    return res.send(
      data.replace(
        '<div id="root"></div>',
        `<div id="root">${ReactDOMServer.renderToString(<YourCustomComponent />)}</div>`
      )
    );
  });
});
```

