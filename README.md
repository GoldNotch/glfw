
# GLFW Bindings for Nim [![Nimble](https://raw.githubusercontent.com/yglukhov/nimble-tag/master/nimble.png)](https://github.com/nim-lang/nimble)

I liked the GLFW binding from NimGL, but I didn't like some deviation from original C API, so I removed all these deviations.
What deviations?
For example set logo by default when window created. Also this logo is private and written in file byte by byte.

Although, OOP-style for GLFWwindow and other objects is good and I didn't changed that.

## Installation
Just clone and import glfw.nim in your code

### Development

It is currently being developed and tested on

* Windows 10
* MacOS Mojave
* Linux Ubuntu 18.10

## Usage

```nim
import glfw

proc keyProc(window: GLFWWindow, key: int32, scancode: int32, action: int32, mods: int32): void {.cdecl.} =
  if key == GLFWKey.Escape and action == GLFWPress:
    window.setWindowShouldClose(true)

proc main() =
  assert glfwInit()

  let w: GLFWWindow = glfwCreateWindow(800, 600, "Title", nil, nil)
  if w == nil:
    quit(-1)

  discard w.setKeyCallback(keyProc)
  w.makeContextCurrent()

  while not w.windowShouldClose:
    glfwPollEvents()
    w.swapBuffers()

  w.destroyWindow()
  glfwTerminate()
  
main()
```

## License

[MIT License](https://github.com/nimgl/nimgl/blob/master/LICENSE)
