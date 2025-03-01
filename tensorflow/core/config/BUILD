load("//tensorflow/core/platform:rules_cc.bzl", "cc_library")
load("//tensorflow:tensorflow.bzl", "tf_cc_test")
load("//tensorflow:tensorflow.bzl", "pytype_strict_library")
load("//tensorflow:tensorflow.bzl", "py_strict_test")
load("//tensorflow:tensorflow.bzl", "tf_python_pybind_extension")

package(
    default_visibility = [
        "//tensorflow/core/config:__subpackages__",
    ],
    licenses = ["notice"],
)

cc_library(
    name = "flags_headers",
    textual_hdrs = [
        "flag_defs.h",
        "flags.h",
    ],
    visibility = ["//tensorflow:internal"],
)

cc_library(
    name = "flag_defs",
    srcs = ["flag_defs.cc"],
    hdrs = ["flag_defs.h"],
    visibility = ["//tensorflow:internal"],
    deps = [
        ":flags",
    ],
)

cc_library(
    name = "flags",
    srcs = ["flags.cc"],
    hdrs = ["flags.h"],
    visibility = ["//tensorflow:internal"],
    deps = [
        "//tensorflow/core/platform:stringpiece",
        "//tensorflow/core/util:env_var",
        "@com_google_absl//absl/strings",
    ],
)

tf_cc_test(
    name = "flags_test",
    srcs = ["flags_test.cc"],
    deps = [
        ":flag_defs",
        ":flags",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
    ],
)

pytype_strict_library(
    name = "flags_py",
    srcs = ["flags.py"],
    srcs_version = "PY3",
    visibility = ["//tensorflow:internal"],
    deps = [
        ":flags_pybind",
        "//tensorflow/python:pywrap_tensorflow",
    ],
)

py_strict_test(
    name = "flags_py_test",
    size = "small",
    srcs = ["flags_test.py"],
    main = "flags_test.py",
    python_version = "PY3",
    tags = ["no_pip"],
    deps = [
        ":flags_py",
        "//tensorflow/python:client_testlib",
    ],
)

tf_python_pybind_extension(
    name = "flags_pybind",
    srcs = ["flags_api_wrapper.cc"],
    module_name = "flags_pybind",
    deps = [
        "//tensorflow/core:lib_headers_for_pybind",
        "//tensorflow/core/config:flags_headers",
        "//tensorflow/python:pybind11_lib",
        "//third_party/python_runtime:headers",
        "@com_google_absl//absl/types:optional",
        "@pybind11",
    ],
)
