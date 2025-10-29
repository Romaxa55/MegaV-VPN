# Contributing to MegaV VPN

First off, thanks for taking the time to contribute! 🎉

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues. When you create a bug report, include as many details as possible:

- OS and version
- VPN client version
- Steps to reproduce
- Expected vs actual behavior
- Logs (if applicable)

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, include:

- Clear and descriptive title
- Detailed description of the suggested enhancement
- Explain why this enhancement would be useful

### Pull Requests

- Fill in the required template
- Follow the Go coding style
- Include appropriate test coverage
- Update documentation as needed

## Development Setup

```bash
# Clone the repo
git clone https://github.com/Romaxa55/MegaV-VPN.git
cd MegaV-VPN

# Install dependencies
go mod download

# Run tests
go test ./...

# Build
go build -o megav cmd/main.go
```

## Code Style

- Use `gofmt` to format code
- Run `golint` before committing
- Keep functions small and focused
- Write descriptive commit messages

## Commit Messages

- Use present tense ("Add feature" not "Added feature")
- Use imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit first line to 72 characters
- Reference issues and pull requests

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

