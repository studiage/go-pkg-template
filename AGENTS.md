# AGENTS.md

This file provides guidance to AI agents when working with code in this repository.

## Project Conventions

### Commenting

#### Golang

- Only document at interface, struct, function level. Not in implementation level.
- Look at other doc comments in the same package for reference.
- All comments should be in lowercase.
- All comments should be in English.
- Follow standard Go commenting conventions

### Error Handling

- Use standard Go `errors` package for error handling if possible
- Use standard Go wrapper functions for error handling if possible, but do not overuse them

### Testing

#### Golang

- Use `ginkgo` for testing.
- Use `gomega` for assertions.
- Use `gomega/gstruct` for struct comparison.
- Always testing with ginkgo in Golang, run `ginkgo -v` to run tests
- Avoid using `time.Sleep` in test, use `Eventually` or `Consistently` instead.
- Each test `It` should wrap with `SpecContext` and `NodeTimeout` to provide context and grouping.
- Having only one parent node per file (var _ = Describe(...)) is recommended to avoid confusion.
- For simple logic, just add 2-3 test cases is enough.
- Trying to follow other tests patterns in the same package.
- Must updates related test files when changing the code firstly, then verify them, but within
related module/package only. No need to verify the whole project.

## Go Development Commands

### Build and Test

- `go build ./...` - Build all Go packages
- `ginkgo -v ./...` - Run all tests
- `ginkgo -v ./path/to/package` - Run tests for a specific package with verbose output
- `ginkgo --focus TestName` - Run a specific test
- `go vet ./...` - Run static analysis
- `go fmt ./...` - Format Go code

### Code Generation

The project uses several code generation tools that must be run when making changes:

- `go generate ./...` - Run all code generation (includes mocks, SQL, Avro schemas, validators)
- `go generate ./internal/database` - Generate SQL queries using sqlc
- `go generate ./internal/events/subscription` - Generate Avro event schemas
- `go generate ./internal/commands` - Generate validation code
- `go generate ./internal/psp/*/mock` - Generate mocks for payment service providers
