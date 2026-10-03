load("@protobuf//bazel:proto_library.bzl", "proto_library")
load("@rules_apple//apple:macos.bzl", "macos_command_line_application")
load("@rules_swift//proto:swift_proto_library.bzl", "swift_proto_library")
load("@rules_swift//swift:swift_library.bzl", "swift_library")
load("@sourcekit_bazel_bsp//rules:setup_sourcekit_bsp.bzl", "setup_sourcekit_bsp")

proto_library(
    name = "addressbook_proto",
    srcs = ["addressbook.proto"],
)

swift_proto_library(
    name = "AddressbookProto_swift",
    protos = [":addressbook_proto"],
)

swift_library(
    name = "main",
    srcs = [
        "main.swift",
    ],
    deps = ["AddressbookProto_swift"],
)

# Top-level target; sourcekit-bazel-bsp indexes libraries through one.
macos_command_line_application(
    name = "app",
    minimum_os_version = "13.0",
    visibility = ["//.bsp/skbsp_generated:__pkg__"],
    deps = [":main"],
)

setup_sourcekit_bsp(
    name = "setup_sourcekit_bsp",
    files_to_watch = ["**/*.swift"],
    index_flags = ["config=index_build"],
    targets = ["//:app"],
)
