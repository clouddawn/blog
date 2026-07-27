# 在 uniapp 跨端开发中，如何处理不同平台的差异化？

在 uniapp 里处理跨端差异化主要有两种方式：一种是用条件编译，比如 `#ifdef MP-WEIXIN`、`#ifdef H5`，这样可以在编译阶段就裁剪掉不需要的代码；另一种是运行时判断，比如用 `uni.getSystemInfoSync()` 获取平台信息，然后做兼容处理。实际开发中，我会结合两者，并把差异逻辑封装成工具函数，这样业务代码可以保持统一，维护性更高。

一般先用 `#ifdef` 区分 APP、小程序、H5，再在 APP 内部用 `getSystemInfoSync` 区分 ios / android。

