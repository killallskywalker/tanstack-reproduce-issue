# Reproduction Steps ( Working Version )
1 . Clone the repository and install dependencies
2 . npm install
3 . npm run build
4 . node .output/server/index.mjs 
5 . Go to localhost:3000

Result: The app runs correctly, and all hashed assets (CSS/JS) match as expected.
No FOUC is observed.

# Reproduction Steps ( FOUC Issue )
1 . Clone the repository
2 . docker compose up 
3 . Go to localhost:3000

Result : The built CSS asset hash use in appCss constant is different . You can check like this to confirm inside the container 

```
# you can get hash value from browser where it 404 
grep -r "your-404-style.css hash value"

# example
grep -r "DvnbdLl" .
./.output/server/chunks/_/router-CyjUN0J9.mjs:const appCss = "/assets/styles-EPdyKHIK.css";


# then you can check the styles that are success since in browser you can see there two style are loaded 
grep -r "your-200-style.css hash value" 

# example 
grep -r "DvnbdLl" .
./.output/server/chunks/nitro/nitro.mjs:  "/assets/styles-DvnbdLl-.css":
```

you can see the hash is different compare when you build in local , you appCss value will have consistent hash .