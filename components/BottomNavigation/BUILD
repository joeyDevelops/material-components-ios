# Copyright 2017-present The Material Components for iOS Authors. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
# implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load(
    "//:material_components_ios.bzl",
    "mdc_extension_objc_library",
    "mdc_objc_library",
    "mdc_public_objc_library",
    "mdc_snapshot_objc_library",
    "mdc_snapshot_test",
    "mdc_unit_test_suite",
)
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")
load("@build_bazel_rules_apple//apple:ios.bzl", "ios_unit_test")

licenses(["notice"])  # Apache 2.0

mdc_objc_library(
    name = "BottomNavigation",
    srcs =
        native.glob(
            [
                "src/*.m",
                "src/private/*.h",
                "src/private/*.m",
            ],
            exclude = [
                "src/MDCBottomNavigationBarController.m",
                "src/MDCBottomNavigationBarController.h",
                "src/MaterialBottomNavigationBeta.h",
            ],
        ),
    hdrs =
        native.glob(
            ["src/*.h"],
            exclude = [
                "src/MDCBottomNavigationBarController.h",
                "src/MaterialBottomNavigationBeta.h",
            ],
        ),
    bundles = [":Bundle"],
    enable_modules = 1,
    includes = ["src"],
    sdk_frameworks = [
        "CoreGraphics",
        "UIKit",
    ],
    visibility = ["//visibility:public"],
    deps = [
        "//components/Ink",
        "//components/Palettes",
        "//components/ShadowElevations",
        "//components/ShadowLayer",
        "//components/Typography",
        "//components/private/Math",
        "@material_internationalization_ios//:MDFInternationalization",
    ],
)

mdc_objc_library(
    name = "BottomNavigationBeta",
    srcs = ["src/MDCBottomNavigationBarController.m"],
    hdrs = [
        "src/MDCBottomNavigationBarController.h",
        "src/MaterialBottomNavigationBeta.h",
    ],
    enable_modules = 1,
    includes = ["src"],
    sdk_frameworks = ["CoreGraphics"],
    visibility = ["//:__subpackages__"],
    deps = [":BottomNavigation"],
)

filegroup(
    name = "BundleFiles",
    srcs = glob([
        "src/MaterialBottomNavigation.bundle/**",
    ]),
)

objc_bundle(
    name = "Bundle",
    bundle_imports = [":BundleFiles"],
)

mdc_extension_objc_library(
    name = "ColorThemer",
    deps = [
        ":BottomNavigation",
        "//components/schemes/Color",
    ],
)

mdc_extension_objc_library(
    name = "TypographyThemer",
    deps = [
        ":BottomNavigation",
        "//components/schemes/Typography",
    ],
)

mdc_objc_library(
    name = "private",
    hdrs = native.glob(["src/private/*.h"]),
    includes = ["src/private"],
    visibility = ["//visibility:private"],
)

mdc_objc_library(
    name = "ObjcExamples",
    srcs = native.glob([
        "examples/*.m",
        "examples/*.h",
        "examples/supplemental/*.m",
        "examples/supplemental/*.h",
    ]),
    includes = ["examples/supplemental"],
    deps = [
        ":BottomNavigation",
        ":ColorThemer",
        ":TypographyThemer",
        "//components/Palettes",
        "//components/schemes/Color",
        "//components/schemes/Typography",
    ],
)

swift_library(
    name = "SwiftExamples",
    srcs = native.glob(
        [
            "examples/*.swift",
            "examples/supplemental/*.swift",
        ],
    ),
    copts = [
        "-swift-version",
        "4.2",
    ],
    deps = [
        ":BottomNavigationBeta",
        ":BottomNavigation",
        ":ColorThemer",
        ":ObjcExamples",
        ":TypographyThemer",
        "//components/AppBar",
        "//components/Buttons",
        "//components/Palettes",
    ],
)

mdc_objc_library(
    name = "unit_test_sources",
    testonly = 1,
    srcs = native.glob(
        [
            "tests/unit/*.m",
            "tests/unit/*.h",
        ],
        exclude = ["tests/unit/MDCBottomNavigationBarControllerTests.m"],
    ),
    sdk_frameworks = [
        "CoreGraphics",
        "XCTest",
    ],
    visibility = ["//visibility:private"],
    deps = [
        ":BottomNavigation",
        ":ColorThemer",
        ":TypographyThemer",
        ":private",
    ],
)

mdc_objc_library(
    name = "unit_test_beta_sources",
    testonly = 1,
    srcs = ["tests/unit/MDCBottomNavigationBarControllerTests.m"],
    sdk_frameworks = [
        "CoreGraphics",
        "XCTest",
    ],
    visibility = ["//visibility:private"],
    deps = [
        ":BottomNavigationBeta",
    ],
)

ios_unit_test(
    name = "unit_tests_beta",
    deps = [":unit_test_beta_sources"],
    minimum_os_version = "9.0",
    flaky = 1,
    test_host = "//components/private/Snapshot/TestHost",
)

mdc_unit_test_suite(
    name = "unit_tests",
    deps = [
        ":unit_test_sources",
    ],
)

mdc_snapshot_objc_library(
    name = "snapshot_test_lib",
    deps = [
        ":BottomNavigation",
        ":ColorThemer",
        ":TypographyThemer",
        ":private",
    ],
)

mdc_snapshot_test(
    name = "snapshot_tests",
    deps = [":snapshot_test_lib"],
)
