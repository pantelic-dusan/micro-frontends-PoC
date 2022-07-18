# micro-frontends-PoC

## HOW TO RUN AND TEST
2. Open new terminal, navigate to repository and run ```cd navigation && npm start```
3. Open new terminal, navigate to repository and run ```cd mf1 && npm start```
4. Open new terminal, navigate to repository and run ```cd mf2 && npm start```
5. Open new terminal, navigate to repository, run ```cd container && npm start``` and open link provided to test app

## CREATING ROOT CONTAINER APP
1. Run ```create-single-spa``` command 
   1. Provide app directory (e.g. container)
   2. Select single-spa root config option
   3. Select npm package manager
   4. Confirm TypeScript usage
   5. Confirm single-spa Layout Engine usage
   6. Provide organisation name (e.g. meas)
2. Run ```npm start``` to check if everything works as expected (You should see welcome single-spa page).

## CREATING BASIC MICRO FRONTEND:
1. Run ```create-single-spa``` command
   1. Provide app directory (e.g. navigation)
   2. Select single-spa application / parcel option
   3. Select desired framework react (or other you want to use)
   4. Select npm package manager
   5. Confirm TypeScript usage
   6. Provide organisation name (e.g. meas)
   7. Provide project name (e.g. navigation)
   8. Run ```npm run start:standalone``` and if everything works You should see page with text that your micro frontend is mounted (e.g. @meas/navigation is mounted!).

## CONNECTING MICRO FRONTEND TO ROOT CONTAINER
   1. Open terminal, navigate to root container and run ```npm start```
      1. If this is not the FIRST import of micro frontend You don't need to do this again.
      2. On single-spa welcome page you will se provided links for shared react dependencies in Next Steps chapter of page.
      3. Navigate to src/index.ejs of root container and find shared ```<script type="systemjs-importmap">``` (try to find where the ```"single-spa"``` is imported because there are multiple import maps).
      4. After ````"single-spa"```` import copy and paste shared react dependencies imports provided on single-spa welcome page.
   2. Open another terminal, navigate to micro frontend (e.g. navigation) and run ```npm start```
      1. When open page You will see that micro frontend is not there and steps how to connect it to root container. We won't use steps described there because with them every developer would need to do them  locally (imports are saved in local storage and not in config files like we will do).
      2. Copy entry link of micro frontend provided in first step on the micro frontend page (e.g. http://localhost:8080/meas-navigation.js)
      3. Navigate to src/index.ejs of root container and find local ```<script type="systemjs-importmap">``` (try to find where the ```@single-spa/welcome``` or some other of Your micro frontends are imported  because there are multiple import maps).
      4. We can now delete ```e``` import and above add import of our micro frontend in format ```"@organisation-name/mf-name": "mf-entry-url"``` (e.g. ```"@meas/navigation": "http://localhost:8080/meas-navigation.js"```).
      5. NOTE: Those import maps are for local development and won't work for production deployment (There is different procedure for deployment).
   3. Navigate to ```src/microfrontend-layout.html``` of root container and use your micro frontend on desired ```<route>``` or on all pages(without ```<route>``` tag). For first time You can replace ```<application name="@single-spa/welcome"></application>``` with your micro frontend application (e.g. ```<application name="@meas/navigation"></application>```).

