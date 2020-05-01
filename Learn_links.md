## 官方资源

主页：https://www.khronos.org/opencl/resources

KhronosGroup的GitHub库

https://github.com/KhronosGroup/Khronosdotorg


## 开源实现

https://github.com/zuzuf/freeocl

## 头文件

以前版本的头文件需要去独立的分支中寻找

https://github.com/KhronosGroup/OpenCL-Headers/tree/56eda020bdd90a4a74dca06b83b90cef820fcc5c

主github库

https://github.com/KhronosGroup/OpenCL-Headers

## 其他知识点

### OpenCL Installable Client Driver (ICD) Loader

OpenCL Installable Client Driver (ICD) Loader是实现OpenCL应用程序与各硬件厂商提供的OpenCL驱动(platform)之间隔离的中间库。

从OpenCL 1.2开始，OpenCL提供了一个ICD扩展(cl_khr_icd),它允许不同厂商的多个OpenCL驱动(platform)共存于一个主机系统，应用程序可以通过调用clIcdGetPlatformIDsKHR函数获取所有已经安装的platform的列表,自由选择使用其中的一个platform。
OpenCL Installable Client Driver (ICD) Loader实现了ICD扩展(cl_khr_icd)并提供了所有OpenCL API接口，应用程序可以通过OpenCL Installable Client Driver (ICD) Loader从已经安装的OpenCL驱动(platform)中选择使用一个平台，应用程序的所有OpenCL API请求将被转发到指定的平台。

简单的说，这个Loader Library只是个二传手，它提供了所有OpenCL API的接口，但没有提供实现，所有通过Loader Library调用的OpenCL API请求都会被传递到指定的OpenCL驱动。有了这个中间库，你的项目代码中的OpenCL API请求可以不依赖于任何厂商的OpenCL SDK,可以在没有安装任何OpenCL SDK的环境实现代码编译，你可以以动态库的形式使用它，也可以把这个中间库静态编译到自己的项目代码中，真正的实现OpenCL SDK无关性、设备无关性。

具体可以参考： https://blog.csdn.net/10km/article/details/50495452

### 开发之前建议先去查看对应标准的文档

https://www.khronos.org/registry/OpenCL/



## 笔者学习链接

可以使用OneTab进行导入

https://www.google.com.hk/search?sxsrf=ALeKk03JqhKh2VT5WeebDopuTMRil7Dsqg%3A1588292312705&ei=2GqrXrrZKvqJr7wP-Kch&q=implement+openCL+standard&oq=implement+openCL+standard&gs_lcp=CgZwc3ktYWIQAzIHCCEQChCgATIHCCEQChCgATIHCCEQChCgAToHCCMQ6gIQJzoECCMQJzoCCAA6BwgAEEYQ_wE6BAgAEAo6BAgAEB46BAgAEBM6BggAEB4QEzoICAAQCBAeEBM6CAgAEAUQHhATOggIABAIEA0QHjoICAAQDRAFEB46CggAEAgQDRAKEB5QxN4NWKqTD2Chlg9oBXAAeAKAAZQIiAGSbpIBCDMtMzYuNy0xmAEAoAEBqgEHZ3dzLXdperABCg&sclient=psy-ab&ved=0ahUKEwi6peT4sZHpAhX6xIsBHfhTCAAQ4dUDCAw&uact=5 | implement openCL standard - Google 搜索
https://en.wikipedia.org/wiki/OpenCL | OpenCL - Wikipedia
https://en.wikipedia.org/wiki/SYCL | SYCL - Wikipedia
https://github.com/KhronosGroup/OpenCL-CTS | KhronosGroup/OpenCL-CTS: The OpenCL Conformance Tests
https://github.com/zuzuf/freeocl | zuzuf/freeocl: Automatically exported from code.google.com/p/freeocl
https://www.khronos.org/opencl/resources | OpenCL Overview - The Khronos Group Inc
https://github.com/KhronosGroup/OpenCL-Headers | KhronosGroup/OpenCL-Headers: Khronos OpenCL-Headers
https://github.com/KhronosGroup/OpenCL-Headers/commits/master?before=3f7c1f77f8e1a3c9b48765c713ca19013e95b91e+35 | Commits · KhronosGroup/OpenCL-Headers
https://github.com/KhronosGroup/OpenCL-Headers/tree/56eda020bdd90a4a74dca06b83b90cef820fcc5c | KhronosGroup/OpenCL-Headers at 56eda020bdd90a4a74dca06b83b90cef820fcc5c
https://github.com/OCL-dev/ocl-icd | OCL-dev/ocl-icd: OpenCL ICD Loader (free software)
https://blog.csdn.net/10km/article/details/50495452 | OpenCL Installable Client Driver (ICD) Loader编译_运维_10km的专栏-CSDN博客
https://www.khronos.org/registry/OpenCL/ | Khronos OpenCL Registry - The Khronos Group Inc
https://github.com/KhronosGroup/OpenCL-Docs | KhronosGroup/OpenCL-Docs: OpenCL API, Extensions, and Environment Spec sources.
https://github.com/KhronosGroup/OpenCL-Registry/blob/master/sdk/1.0/docs/OpenCL-1.0-refcard.pdf | OpenCL-Registry/OpenCL-1.0-refcard.pdf at master · KhronosGroup/OpenCL-Registry
https://www.khronos.org/registry/OpenCL/specs/2.2/html/OpenCL_ICD_Installation.html | OpenCL™ ICD Installation Guidelines
https://github.com/KhronosGroup/OpenCL-Docs/tree/master/ext | OpenCL-Docs/ext at master · KhronosGroup/OpenCL-Docs
https://github.com/KhronosGroup/OpenCL-Docs/blob/master/ext/cl_khr_icd.asciidoc | OpenCL-Docs/cl_khr_icd.asciidoc at master · KhronosGroup/OpenCL-Docs
https://www.google.com/search?sxsrf=ALeKk02YYqbXTh-VPHd4C-MZQn6eHDLrFA%3A1588305992897&source=hp&ei=SKCrXoKBNNLFmAX4sLmADQ&q=implement+Vendor+ICD%E2%80%99s+library&oq=implement+Vendor+ICD%E2%80%99s+library&gs_lcp=CgZwc3ktYWIQAzoCCAA6BwgAEEYQ_wFQxRJYhjNg_DhoAXAAeACAAb8DiAHOIZIBBTMtNy40mAEAoAEBoAECqgEHZ3dzLXdpeg&sclient=psy-ab&ved=0ahUKEwiCxf7z5JHpAhXSIqYKHXhYDtAQ4dUDCAc&uact=5 | implement Vendor ICD’s library - Google 搜索
https://www.khronos.org/registry/OpenCL/sdk/2.1/docs/man/xhtml/cl_khr_icd.html | cl_khr_icd
https://www.khronos.org/registry/OpenCL/specs/ | www.khronos.org:/registry/OpenCL/specs/
https://www.khronos.org/registry/OpenCL/ | Khronos OpenCL Registry - The Khronos Group Inc