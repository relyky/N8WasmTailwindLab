# N8WasmTailwindLab
 NET8 + Blazor WASM + Tailwind CSS   
 > 懶得寫了。附上相關材料。俱體請參考文件。

# 參考文件
* [Building beautiful Blazor apps with Tailwind CSS | .NET Conf 2023](https://www.youtube.com/watch?v=QIdedo8iI4Y)
* [Blazor & Tailwind CSS 🔥 Quick Start Guide](https://www.youtube.com/watch?v=tj4dNN2jQt0) 

# 終端機 \ npm 指令
```bash
## init
> npx tailwindcss init

## dev mode
> npx tailwindcss -i .\Styles\app.css -o .\wwwroot\css\app.css --watch

## release mode
> npx tailwindcss -i .\Styles\app.css -o .\wwwroot\css\app.css --minify
```

# tailwind.config.js
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./**/*.{razor,html}'],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

# YourWasmProject.csproj
``` xml
<Target Name="CheckForNpm" BeforeTargets="BuildCSS">
  <Exec Command="npm -v" ContinueOnError="true">
    <Output TaskParameter="ExitCode" PropertyName="ErrorCode" />
  </Exec>
  <Error Condition="'$(ErrorCode)' != '0'" Text="You must install NPM to build this project" />
</Target>

<Target Name="BuildCSS" BeforeTargets="Compile">
  <Exec EnvironmentVariables="NODE_ENV=production"
        Command="npx tailwindcss -i Styles/app.css -o wwwroot/css/app.css --minify"
		Condition=" '$(Configuration)' == 'Release' " />
</Target>
```
