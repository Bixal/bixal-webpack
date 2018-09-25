# Set up your decoupled environment:
1. Create apps using create-react-app or place in /apps.
2. Merge the package.json files to ./package.json and delete them from the individual apps.
3. Run: 'npm install'
4. Create a block for your app in: web/modules/custom/YOURMODULE/src/Plugin/Block/.
5. Run: 'npm run build'
6. Add app to YOURMODULE.libraries.yml.
