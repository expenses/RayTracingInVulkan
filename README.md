# Ray Tracing In Vulkan

My implementation of [Peter Shirley's Ray Tracing in One Weekend](https://github.com/petershirley/raytracinginoneweekend) book using Vulkan and NVIDIA's RTX extension (VK_NV_ray_tracing). This allows most scenes to render at interactive speed on appropriate hardware.

This real-time ray tracer can also load full geometry from OBJ files as well as render the procedural spheres from the book. An accumulation buffer is used to increase the sample count when the camera is not moving while keeping the frame rate interactive. I have added a UI built using [Dear ImGui](https://github.com/ocornut/imgui) to allow changing the renderer parameters on the fly. Unlike projects such as [Q2VKPT](http://brechpunkt.de/q2vkpt/), there is no denoising filter. So the image will get noisy when moving the camera.

This personal project follows my own attempts at CPU ray tracing following Peter Shirley's books (see [here](https://github.com/GPSnoopy/RayTracingInOneWeekend) and [here](https://github.com/GPSnoopy/RayTracingTheNextWeek) if you are interested).

## TODOs

I do intend on implementing the scenes from the second book [Ray Tracing The Next Week](https://github.com/petershirley/raytracingthenextweek) when I get the time. 

## Performance

Using a GeForce RTX 2080 Ti, the rendering speed is obscenely faster than using the CPU renderer. Obviously both implementations are still quite naive in some places, but I'm really impressed by the performance. The cover scene of the first book reaches ~90fps at 1280x720 using 8 rays per pixel and up to 16 bounces.

I suspect performance could be improved further. I have created each object in the scene as a separate instance in the top level acceleration structure, which is probably not the best for data locality. The same goes displaying multiple [Lucy statues](http://graphics.stanford.edu/data/3Dscanrep/), where I have naively duplicated the geometry rather than instancing it multiple times.

## Building

Most of the third party dependencies can be built using [Microsoft's vcpkg](https://github.com/Microsoft/vcpkg).

**Windows (Visual Studio 2017 Win64 solution)**
```
> vcpkg_windows.bat
> build_windows.bat
```
**Linux (GCC 8 Makefile)**
```
> ./vcpkg_linux.sh
> ./build_linux.sh
```

Assuming you have installed the [Vulkan SDK](https://vulkan.lunarg.com/), the build should work out-of-the box for Visual Studio. On Linux, you may have to manually install additional dependencies for `vcpkg_linux.sh` to succeed.

## References

* [Vulkan Tutorial] (https://vulkan-tutorial.com/)
* [Introduction to Real-Time Ray Tracing with Vulkan](https://devblogs.nvidia.com/vulkan-raytracing/)
* [NVIDIA Vulkan Ray Tracing Tutorial] (https://developer.nvidia.com/rtx/raytracing/vkray)
* [NVIDIA Vulkan Ray Tracing Helpers: Introduction] (https://developer.nvidia.com/rtx/raytracing/vkray_helpers)
* [Fast and Fun: My First Real-Time Ray Tracing Demo] (https://devblogs.nvidia.com/my-first-ray-tracing-demo/)
* [D3D12 Raytracing Samples] (https://github.com/Microsoft/DirectX-Graphics-Samples/tree/master/Samples/Desktop/D3D12Raytracing)
* [George Ouzounoudis's vk_exp] (https://github.com/georgeouzou/vk_exp)
* [NVIDIA Vulkan Forums] (https://devtalk.nvidia.com/default/board/166/vulkan/)
