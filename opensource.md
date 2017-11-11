---
layout: page
title: Open Source
permalink: /opensource/
tags: opensource
---

In this section I usually post about the bugs which I fixed during my open source contributions:

## Mozilla Firefox

* Bug 1294466 - Check that the output of all JITFLAGS is the same on jit-tests
* Bug 637400 - Check that the output of all JITFLAGS tests is the same
* Bug 1290676 - Call InsertionSort when denseLen < 24 in MergeSort?
* Bug 1284441 - Remove unnecessary cast from ExpressionDecompiler::decompilePC.
* Bug 1238801 - Don't bother setting a timer that will never fire in nsGeolocationRequest::SetTimeoutTimer()
* Bug 1155342 - Disallow flagging [NewObject] methods with [Pure] or [Constant] or the corresponding [DependsOn] values
* Bug 1142826 - js/src/jsapi-tests/testMutedErrors.cpp has leaks
* Bug 1142820 - js/src/jsapi-tests/testPersistentRooted.cpp has leaks
* Bug 1142816 - js/src/jsapi-tests/testGCHeapPostBarriers.cpp has leaks
* Bug 1104156 - TCPSocket doesn't close output stream until all buffered streams in the multiplex stream are sent
* Bug 1021963 - Self-host isNaN and isFinite, relying on Number_isNaN and Number_isFinite for implementation
* Bug 1296176 - Replace PR_MIN with std::min in netwerk
* Bug 1276701 - Remove Windows code from Safari migrator