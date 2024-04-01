# Steps to add Tailwind in MVC 7 projects:
## Step 0:
Create the project (Visual Studio in the example)

## Step 1:
Open the terminal within the project folder and start a node project
```
npm init -y
```
## Step 2:
Add Tailwind
```
npm install -D tailwindcss
```
## Step 3:
Add the following script to package.json (for the css output location)
```
"scripts": {
    "css:build": "npx tailwindcss -i ./wwwroot/css/site.css -o ./wwwroot/css/styles.css --minify"
  }
```
## Step 4:
Init the tailwind config file
```
npx tailwindcss init
```
## Step 5:
Add modules to tailwind.config.json
```
module.exports = {
    content: [
       './Pages/**/*.cshtml',
       './Views/**/*.cshtml'
],
    theme: {
        extend: {},
    },
    plugins: [],
}
```
## Step 6:
Add input css to site.css (default css class) in wwwroot/css (or in your main css)
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
## Step 7:
Add itemgroups in the project under the .csproj file (double click in the second line in the Solution Explorer View). This is for building the css before deploying.
```
<ItemGroup>
  <UpToDateCheckBuilt Include="wwwroot/css/site.css" Set="Css" />
  <UpToDateCheckBuilt Include="tailwind.config.js" Set="Css" />
</ItemGroup>

<Target Name="Tailwind" BeforeTargets="Build">
  <Exec Command="npm run css:build"/>
</Target>
```
![Solution Explorer image](https://live.staticflickr.com/65535/53625050224_9e6d1b7d3a_w.jpg)
## Step 8:
Include the path to the CSS file in the _Layout.cshtml file (Or others views you need to style with tailwind)
```
<link rel="stylesheet" href="~/css/styles.css" asp-append-version="true" />
```
## Final:
You are ready to use Tailwind in your project. Here's a small code snippet to try out:
```
<div class="bg-red-500 w-20 h-20"></div>
```
