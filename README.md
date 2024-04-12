## Creating a helloworld snap-in

There was no reference to what a helloworld snap-in was, so here we have console logged "Hello world" whenever a new workitem is created 

### Steps to create a snap-in
1. download Devrev CLI and jq
2. Next authenticate yourself using: (org-slug is basically the org name user is associated with) 
 ```
 devrev profiles authenticate -o <dev-org-slug> -u <youremail@yourdomain.com>
 ```
3. Now create a folder and run the following command in the terminal of that directory
```
devrev snap_in_version init
```
4. This will create a snap-in template codein that folder
5. There will be many files/folders in the template, but our main focus is on just few files
6. First is manifest.yaml, here we define the name of our snap-in, its description,functions and event(command/automation) etc
7. Now based on the fuctions defined in this .yaml, we define the fuctions in the function folder
8. Here for hello_world snap-in 

### Testing locally
You can test your code by adding test events under `src/fixtures` similar to the example event provided. You can add keyring values to the event payload to test API calls as well.

Once you have added the event, you can test your code by running:
```
npm install
npm run start -- --functionName=on_work_creation --fixturePath=on_work_created_event.json
```

### Adding external dependencies
You can also add dependencies on external packages in package.json under the “dependencies” key. These dependencies will be made available to your function at runtime and testing.

### Linting

To check for lint errors, run the following command:

```bash
npm run lint
```

To automatically fix fixable lint errors, run:

```bash
npm run lint:fix
```

### Deploying Snap-Ins
Once you are done with the testing, run the following commands to deploy your snap_in:

1. Authenticate to devrev CLI
```
devrev profiles authenticate --org <devorg name> --usr <user email>
```
2. Create a snap_in_version
```
devrev snap_in_version create-one --path <template path> --create-package
```
3. Draft the snap_in
```
devrev snap_in draft
```
4. Update the snap_in
```
devrev snap_in update
```
5. Deploy the snap_in
```
devrev snap_in deploy
```
