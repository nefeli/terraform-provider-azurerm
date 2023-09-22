load("@io_bazel_rules_go//go:def.bzl", "go_binary", "go_library")
load("@bazel_gazelle//:def.bzl", "gazelle")

# gazelle:prefix github.com/hashicorp/terraform-provider-azurerm
gazelle(name = "gazelle")

gazelle(
    name = "gazelle-update-repos",
    args = [
        "-from_file=go.mod",
        "-to_macro=deps.bzl%go_dependencies",
        "-prune",
        "-index=false",
        "-build_file_proto_mode=disable",
    ],
    command = "update-repos",
)

go_library(
    name = "terraform-provider-azurerm_lib",
    srcs = ["main.go"],
    importpath = "github.com/hashicorp/terraform-provider-azurerm",
    visibility = ["//visibility:private"],
    deps = [
        "//internal/provider",
        "//vendor/github.com/hashicorp/terraform-plugin-sdk/v2/plugin",
    ],
)

go_binary(
    name = "terraform-provider-azurerm",
    embed = [":terraform-provider-azurerm_lib"],
    visibility = ["//visibility:public"],
)
