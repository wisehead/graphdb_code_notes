#1.main

```
main
--QueryServiceExecutor::instance().block_on(async_main());
```

#2.call stack

```
arcgraph_server::main (/home/chenhui/gitee/fabarta-db/src/main.rs:90)
core::ops::function::FnOnce::call_once (@core::ops::function::FnOnce::call_once:6)
std::sys_common::backtrace::__rust_begin_short_backtrace (@std::sys_common::backtrace::__rust_begin_short_backtrace:6)
std::rt::lang_start::{{closure}} (@std::rt::lang_start::{{closure}}:7)
core::ops::function::impls::<impl core::ops::function::FnOnce<A> for &F>::call_once (@std::rt::lang_start_internal:222)
std::panicking::try::do_call (@std::rt::lang_start_internal:221)
std::panicking::try (@std::rt::lang_start_internal:221)
std::panic::catch_unwind (@std::rt::lang_start_internal:221)
std::rt::lang_start_internal::{{closure}} (@std::rt::lang_start_internal:221)
std::panicking::try::do_call (@std::rt::lang_start_internal:221)
std::panicking::try (@std::rt::lang_start_internal:221)
std::panic::catch_unwind (@std::rt::lang_start_internal:221)
std::rt::lang_start_internal (@std::rt::lang_start_internal:221)
std::rt::lang_start (@std::rt::lang_start:13)
main (@main:10)
__libc_start_main (@__libc_start_main:64)
_start (@_start:15)

```