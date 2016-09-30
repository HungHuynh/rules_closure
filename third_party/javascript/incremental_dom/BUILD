# Copyright 2016 The Closure Rules Authors. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

licenses(["notice"])  # Apache License Version 2.0

load("//closure:defs.bzl", "closure_js_library")

closure_js_library(
    name = "incremental_dom",
    srcs = ["incremental-dom-closure.js"],
    language = "ECMASCRIPT6_STRICT",
    visibility = ["//visibility:public"],
)

genrule(
    name = "extract",
    srcs = ["@incremental_dom//file"],
    outs = ["incremental-dom-closure.js"],
    cmd = " && ".join([
        "IN=$$(pwd)/$(SRCS)",
        "OUT=$$(pwd)/$@",
        "TMP=$$(mktemp -d $${TMPDIR:-/tmp}/genrule.XXXXXXXXXX)",
        "SCRIPT=$$(pwd)/$(location :build)",
        "cd $$TMP",
        "$$SCRIPT $$IN $$OUT",
        "rm -rf $$TMP",
    ]),
    tools = [":build"],
)

sh_binary(
    name = "build",
    srcs = ["build.sh"],
)