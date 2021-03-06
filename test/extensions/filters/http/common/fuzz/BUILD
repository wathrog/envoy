licenses(["notice"])  # Apache 2

load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_fuzz_test",
    "envoy_package",
    "envoy_proto_library",
)
load(
    "//source/extensions:all_extensions.bzl",
    "envoy_all_extensions",
)

envoy_package()

envoy_proto_library(
    name = "filter_fuzz_proto",
    srcs = ["filter_fuzz.proto"],
    deps = [
        "//test/fuzz:common_proto",
        "@envoy_api//envoy/extensions/filters/network/http_connection_manager/v3:pkg",
    ],
)

envoy_cc_fuzz_test(
    name = "filter_fuzz_test",
    srcs = ["filter_fuzz_test.cc"],
    corpus = "filter_corpus",
    # All Envoy extensions must be linked to the test in order for the fuzzer to pick
    # these up via the NamedHttpFilterConfigFactory.
    deps = [
        ":filter_fuzz_proto_cc_proto",
        "//source/common/config:utility_lib",
        "//source/common/config:version_converter_lib",
        "//source/common/protobuf:utility_lib",
        "//test/config:utility_lib",
        "//test/fuzz:utility_lib",
        "//test/mocks/buffer:buffer_mocks",
        "//test/mocks/http:http_mocks",
        "//test/mocks/server:server_mocks",
    ] + envoy_all_extensions(),
)
