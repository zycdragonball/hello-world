licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

load("//tensorflow:tensorflow.bzl", "tf_custom_op_library")
load("//tensorflow:tensorflow.bzl", "tf_gen_op_libs")
load("//tensorflow:tensorflow.bzl", "tf_gen_op_wrapper_py")
load("//tensorflow:tensorflow.bzl", "tf_custom_op_py_library")

tf_custom_op_library(
    name = "python/ops/_repeat_op.so",
    srcs = [
        "kernels/repeat_op.cc",
        "ops/repeat_op.cc",
    ],
)

tf_gen_op_libs(
    op_lib_names = ["repeat_op"],
)

tf_gen_op_wrapper_py(
    name = "repeat_op",
    deps = [":repeat_op_op_lib"],
)

tf_custom_op_py_library(
    name = "repeat_py",
    srcs = [
        "__init__.py",
        "python/ops/repeat_op.py",
    ],
    dso = [
        ":python/ops/_repeat_op.so",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":repeat_op",
        "//tensorflow/contrib/util:util_py",
        "//tensorflow/python:platform",
        "//third_party/py/numpy",
    ],
    visibility = ["//visibility:public"],
)

py_test(
    name = "repeat_op_test",
    size = "small",
    srcs = ["python/kernel_tests/repeat_op_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":repeat_py",
        "//tensorflow/python:platform_test",
        "//third_party/py/numpy",
    ],
)
    
filegroup(
    name = "all_files",
    srcs = glob(
        ["**/*"],
        exclude = [
            "**/METADATA",
            "**/OWNERS",
        ],
    ),
    visibility = ["//tensorflow:__subpackages__"],
)
