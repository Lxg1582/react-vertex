## `@react-vertex/core - Texture Hooks`

React hooks for working with WebGL textures. More info on [using textures in WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Tutorial/Using_textures_in_WebGL).

##### Install via npm:
```js
npm install @react-vertex/core
```

##### Importing:

```js
import {
  useTexture2d,
} from '@react-vertex/core'
```

#### `useTexture2d(url, getOptions?)` => \[`WebGLTexture`, `isLoaded`\]

React hook for 2d WebGL textures. It returns a texture immediately with a placeholder pixel and updates it when the image loads.

###### Arguments:

`url`: The URL of the texture image to load.

`getOptions (optional)`: A function that will be called with the context (gl) that returns an object with the options you wish to override. The hook does not update when this param changes so you can use an inline function.

###### Valid keys in object returned by getOptions:
  - `format` defualts to gl.RGBA
  - `crossOrigin` defaults to `anonymous` (this is for the image request)
  - `mipMaps`Boolean defaults to true. More on [mipmaps](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext/generateMipmap).
  - `type` defaults to gl.UNSIGNED_BYTE
  - `wrap` defaults to null (sets both wrapS and wrapT)
  - `wrapS` defaults to gl.REPEAT (will be overridden by `wrap` if used)
  - `wrapT` defaults to gl.REPEAT (will be overridden by `wrap` if used)
  - `minMag` defaults to null (sets both minFilter and magFilter)
  - `minFilter` defaults to gl.NEAREST_MIPMAP_LINEAR (will be overridden by `minMag` if used)
  - `magFilter` defaults to gl.LINEAR (will be overridden by `minMag` if used)
  - `placeholder` defaults to a black pixel (new Uint8Array(\[0, 0, 0, 1\]))

###### Returns:

\[`texture`, `isLoaded`\] : An array with a [WebGLTexture](https://developer.mozilla.org/en-US/docs/Web/API/WebGLTexture) as the first item and a boolean `isLoaded` indicating whether the full image has loaded yet.

###### Example Usage:

```js
import { useWebGLContext, useProgram, useTexture2d, useUniformSampler2d } from '@react-vertex/core'

...
  const gl = useWebGLContext()
  const program = useProgram(gl, vert, frag)

  const [texture] = useTexture2d(imageUrl, () => {
    placeholder: new Uint8Array([0, 0, 1, 1])
  })
  useUniformSampler2d(gl, program, 'texDiff', texture)
...

```
