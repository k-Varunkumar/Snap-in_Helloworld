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
7. Now based on the fuctions defined in this .yaml, we define the fuctions in the function folder(which is inside code folder)
8. Here for hello_world snap-in, in the function that we create(or rename the default fn and make necessary changes in related files) in run fn we get all the objects that trigger the event defined in .yaml file. now these events are looped and handleevent() is called.
9. Now for helloworld snapin we write a console.log("hello world") in this handleevent(), so whenever and event is created "hello world is printed"
10. Now in the code directory run the following commands
```
npm install
npm run build
npm run package
```
11. These will install all the node modules and ready the package for deployment
12. Then to create a snap-in package, run the following command:
 ```
 devrev snap_in_package create-one --slug my-first-snap-in | jq .
 ```
13.Then to create a snap-in version, run the following command:(path must be of the parent of code folder) 
```
devrev snap_in_version create-one --path ./devrev-snaps-typescript-template | jq .
```
14. Then to finally create a snap-in from a snap-in version, we run the following command:
```
devrev snap_in draft
```
15. Now this will be installed in our devrev UI, now we have to install it from there
16. so go to settings->snap-in, the name that we have given to our snapin .yaml will be on of the snap-in
17. Install it from there,so now our snap-in is successfully installed, and try it when we create a new workitem 
