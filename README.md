# Skooma Default Template 🧪

![Go Version](https://img.shields.io/badge/Go-1.26.1%2B-00ADD8?logo=go&logoColor=white)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green)

> _"The official default template for Skooma - brewing full-stack magic since day one."_

This is the default project template used by [Skooma](https://github.com/skooma-cli/skooma) to scaffold full-stack single-page applications. It provides a complete development stack with Go/Gin backend, React + TypeScript + Vite + Tailwind CSS frontend, and Docker Compose orchestration.

## What's Included

This template generates a modern, production-ready full-stack application with:

### Backend

- **Go 1.26.1+** with [Gin](https://github.com/gin-gonic/gin) web framework
- **Environment configuration** via [godotenv](https://github.com/joho/godotenv)
- **Database support** for PostgreSQL, Microsoft SQL Server, or flat files
- **Docker** containerization with hot-reload development setup
- **RESTful API** structure ready for expansion

### Frontend

- **React 19** with TypeScript for type safety
- **Vite** for lightning-fast development and builds
- **Tailwind CSS** for utility-first styling
- **ESLint** configuration for code quality
- **Hot module replacement** for instant development feedback

### Infrastructure

- **Docker Compose** orchestration for all services
- **PostgreSQL** database service (configurable)
- **Volume mounting** for development hot-reload
- **Environment variable** management
- **Multi-service** architecture ready for scaling

## Template Structure

```
template/
├── docker-compose.yml.tmpl          # Service orchestration
├── backend/
│   ├── go.mod.tmpl                  # Go module definition
│   ├── main.go.tmpl                 # Backend entry point
│   └── Makefile.tmpl                # Build automation
└── frontend/
    ├── index.html.tmpl              # Main HTML template
    ├── package.json.tmpl            # Node.js dependencies
    ├── vite.config.ts.tmpl          # Vite configuration
    ├── tsconfig.json.tmpl           # TypeScript config (main)
    ├── tsconfig.app.json.tmpl       # TypeScript config (app)
    ├── tsconfig.node.json.tmpl      # TypeScript config (node)
    ├── eslint.config.js.tmpl        # ESLint configuration
    ├── .gitignore.tmpl              # Git ignore patterns
    ├── README.md.tmpl               # Frontend documentation
    ├── public/                      # Static assets
    └── src/
        ├── main.tsx.tmpl            # React entry point
        ├── App.tsx.tmpl             # Main App component
        ├── App.css.tmpl             # App-specific styles
        └── index.css.tmpl           # Global styles
```

## Template Variables

When Skooma processes this template, the following variables are available:

| Variable        | Description                                        | Example                       |
| --------------- | -------------------------------------------------- | ----------------------------- |
| `{{.Name}}`     | Project name (alphanumeric, no spaces/underscores) | `myapp`                       |
| `{{.RepoURL}}`  | Repository URL without protocol                    | `github.com/user/myapp`       |
| `{{.Author}}`   | Author information in Name <email> format          | `John Doe <john@example.com>` |
| `{{.Database}}` | Database type: `file`, `mssql`, or `postgres`      | `postgres`                    |

## Usage

This template is designed to be consumed by the [Skooma CLI tool](https://github.com/skooma-cli/skooma). Users don't typically interact with this repository directly.

### Via Skooma CLI:

```bash
# Interactive mode - will prompt for template selection
skooma brew myapp

# Non-interactive mode with specific template
skooma brew myapp --template default --repo github.com/user/myapp --database postgres
```

### Manual Usage:

If you want to use this template manually:

1. Clone this repository
2. Replace all `{{.Variable}}` placeholders with your actual values
3. Remove the `.tmpl` extensions from all files
4. Run `docker-compose up` to start the development environment

## Generated Project Workflow

Once processed by Skooma, the generated project supports:

### Development:

```bash
# Start all services
docker-compose up

# Backend available at: http://localhost:8080
# Frontend available at: http://localhost:3000
# Database available at: localhost:5432 (if PostgreSQL)
```

### Backend Development:

```bash
cd backend
make build    # Build the Go binary
make run      # Run with hot reload
make test     # Run tests
make clean    # Clean build artifacts
```

### Frontend Development:

```bash
cd frontend
npm install   # Install dependencies
npm run dev   # Start development server
npm run build # Build for production
npm run lint  # Run linting
```

## Generated Project Structure

After running `skooma brew myapp` with this template, you'll find a `myapp/` directory with the following layout:

```
myapp/
├── docker-compose.yml
├── backend/
│   ├── go.mod
│   ├── main.go
│   └── Makefile
└── frontend/
    ├── index.html
    ├── package.json
    ├── vite.config.ts
    ├── tsconfig.json
    ├── tsconfig.app.json
    ├── tsconfig.node.json
    ├── eslint.config.js
    ├── .gitignore
    ├── public/
    └── src/
        ├── main.tsx
        ├── App.tsx
        ├── App.css
        └── index.css
```

## Database Configurations

The template supports multiple database options configured via the `--database` flag:

| Value      | Description                                                                                      |
| ---------- | ------------------------------------------------------------------------------------------------ |
| `file`     | Flat file storage — no database container, no extra dependencies. Good for getting started fast. |
| `mssql`    | Microsoft SQL Server container.                                                                  |
| `postgres` | PostgreSQL container. The default in generated `docker-compose.yml` examples.                    |

The database choice controls what services get configured in `docker-compose.yml` and how your backend connects to data storage.

### PostgreSQL (Default)

- Full PostgreSQL 15 container in Docker Compose
- Connection string: `postgres://postgres:password@db:5432/{{.Name}}`
- Persistent data via Docker volumes

### Microsoft SQL Server

- SQL Server container with developer edition
- Windows authentication disabled
- Custom connection configuration

### Flat File

- No database container required
- File-based storage in the backend
- Ideal for prototyping and simple applications

## Customization

### Adding New Template Variables:

1. Define the variable in Skooma's `ProjectData` structure
2. Add it to the template processing logic
3. Use `{{.YourVariable}}` in any `.tmpl` file

### Modifying the Stack:

- **Backend**: Edit `backend/main.go.tmpl` and `backend/go.mod.tmpl`
- **Frontend**: Modify files in `frontend/src/` and `frontend/package.json.tmpl`
- **Infrastructure**: Update `docker-compose.yml.tmpl`

### Creating Variations:

This template serves as a reference implementation. Create your own templates by:

1. Starting with this structure
2. Modifying the technology stack
3. Adding or removing services in Docker Compose
4. Registering your template with Skooma

## Contributing

When contributing to this template:

1. **Test thoroughly** - Changes affect all new Skooma projects
2. **Maintain backwards compatibility** - Existing template variables should remain functional
3. **Update documentation** - Keep this README synchronized with changes
4. **Follow conventions** - Use consistent naming and structure patterns
5. **Test template variables** - Ensure all `{{.Variable}}` substitutions work correctly

## Requirements

### For Template Usage:

- Skooma CLI tool
- Docker and Docker Compose
- Git (for cloning generated projects)

### For Generated Projects:

- **Backend**: Go 1.26.1+, Make
- **Frontend**: Node.js 18+, npm/yarn/pnpm
- **Infrastructure**: Docker and Docker Compose

## Related Projects

- **[Skooma](https://github.com/skooma-cli/skooma)** - The CLI tool that processes this template
- **[More Templates](https://github.com/mark-rodgers?tab=repositories&q=skooma-template)** - Additional official and community templates

## License

MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <em>May your roads lead you to warm sands... and well-structured codebases. 🏺</em>
</p>
