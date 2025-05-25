---
emoji: 🪿
title: Flutter Gimmicks
description: Fidgeting with flutter and it's internals
date: 2024-03-08
layout: base
---

Flutter comes with super complex build system that ties in all the language runtimes with dart and the native rendering engine. So, naturally there is a tradeoff between having to build all these things and being slow or reusing builds and being fast but occassionally wrong.
Flutter I think, errs on the latter. So, most times when you feel like flutter is not doing something you think it should be doing, it is because the build got messed up.


------------

Flutter dependency problem:

If there is a dependency problem, don't have pinned dependencies and have the dependency resolver do the heavy lifting for you.