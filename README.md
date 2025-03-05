# Bazel GRPC Python bug

I believe that the bug is in the `py_proto_library` rule implementation, which first was introduced there:
https://github.com/grpc/grpc/blob/v1.58.0-pre1/bazel/python_rules.bzl#L193

## Reproduction

### GRPC version 1.70.1

Run `bazel build @com_github_grpc_grpc//src/proto/grpc/testing:empty_py_pb2_grpc` to reproduce the error.

Interesting case, for example `bazel build @com_github_grpc_grpc//src/python/grpcio_health_checking/grpc_health/v1:health_py_pb2_grpc` works fine.

### GRPC version 1.58.0

Uncomment the `http_archive` in the `WORKSPACE` and run the following commands

`bazel build @com_github_grpc_grpc//src/proto/grpc/testing:empty_py_pb2_grpc` works fine.

`bazel build @com_github_grpc_grpc//src/python/grpcio_health_checking/grpc_health/v1:health_py_pb2_grpc` should fail.
