package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

load("//tensorflow:tensorflow.bzl", "cuda_py_test")
load("//tensorflow:tensorflow.bzl", "py_test")
load("//tensorflow:tensorflow.bzl", "tf_py_test")

py_library(
    name = "profiler",
    srcs = ["profiler.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":model_analyzer",
        ":tfprof_logger",
        "//tensorflow/python:util",
    ],
)

py_library(
    name = "model_analyzer",
    srcs = ["model_analyzer.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":tfprof_logger",
        "//tensorflow/core/profiler:protos_all_py",
        "//tensorflow/python:pywrap_tensorflow",
    ],
)

cuda_py_test(
    name = "model_analyzer_test",
    srcs = ["model_analyzer_test.py"],
    additional_deps = [
        ":model_analyzer",
        "//tensorflow/python/profiler/internal:model_analyzer_testlib",
        "//tensorflow/python:client",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:platform",
        "//tensorflow/python:variables",
    ],
    tags = ["no_pip"],
)

cuda_py_test(
    name = "profiler_test",
    srcs = ["profiler_test.py"],
    additional_deps = [
        ":model_analyzer",
        "//tensorflow/python:client",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:platform",
        "//tensorflow/python/profiler/internal:model_analyzer_testlib",
        "//tensorflow/python:variables",
    ],
    tags = ["no_pip"],
)

py_library(
    name = "tfprof_logger",
    srcs = ["tfprof_logger.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/core/profiler:protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:platform",
        "@six_archive//:six",
    ],
)

tf_py_test(
    name = "tfprof_logger_test",
    size = "small",
    srcs = ["tfprof_logger_test.py"],
    additional_deps = [
        ":tfprof_logger",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/core/profiler:protos_all_py",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:math_ops",
    ],
)

py_library(
    name = "pprof_profiler",
    srcs = ["pprof_profiler.py"],
    srcs_version = "PY2AND3",
    deps = ["@com_google_pprof//:pprof_proto_py"],
)

py_test(
    name = "pprof_profiler_test",
    size = "small",
    srcs = ["pprof_profiler_test.py"],
    main = "pprof_profiler_test.py",
    srcs_version = "PY2AND3",
    tags = ["no_pip"],  # TODO(annarev): get it working with pip.
    deps = [
        ":pprof_profiler",
        "//tensorflow/python:client",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:platform_test",
        "@com_google_pprof//:pprof_proto_py",
    ],
)

# -----------------------------------------------------------------------------
# Google-internal targets.  These must be at the end for syncrepo.

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
