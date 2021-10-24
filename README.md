# go-devcontainer-template

 Docker container as a full-featured VS Code Go development environment 

## Project Structure

This is a basic layout for Go application projects. Clone the repository, keep what you need and delete everything else! Just because it's there it doesn't mean you have to use it all. None of these patterns are used in every single project.

I find many Go projects also end up hosting pretty much all their code at the root level of the repo. This easily makes the repository a complete mess when I try to look at the code and it is just one big mess in the top directory.

With Go 1.14 [`Go Modules`](https://github.com/golang/go/wiki/Modules) are finally ready for production. Use [`Go Modules`](https://blog.golang.org/using-go-modules) unless you have a specific reason not to use them and if you do then you don’t need to worry about $GOPATH and where you put your project.

### `/cmd`

Main applications for this project.

The directory name for each application should match the name of the executable you want to have (e.g., `/cmd/myapp`).

Don't put a lot of code in the application directory. If you think the code can be imported and used in other projects, then it should live in the `/pkg` directory. If the code is not reusable or if you don't want others to reuse it, put that code in the `/internal` directory. You'll be surprised what others will do, so be explicit about your intentions!

It's common to have a small `main` function that imports and invokes the code from the `/internal` and `/pkg` directories and nothing else.

See the [`/cmd`](cmd/README.md) directory for examples.

### `/api`

OpenAPI/Swagger specs, JSON schema files, protocol definition files.

See the [`/api`](api/README.md) directory for examples.


### `/internal`
This package holds the private library code used in your service, it is specific to the function of the service and not shared with other services. One thing to note is this privacy is enforced by the compiler itself, see the [`Go 1.4 release notes`](https://golang.org/doc/go1.4#internalpackages) for more details. Note that you are not limited to the top level `internal` directory. You can have more than one `internal` directory at any level of your project tree.

See the [`/internal`](internal/README.md) directory for examples.

### `/pkg`
This folder contains code which is OK for other services to consume, this may include API clients, or utility functions which may be handy for other projects but don’t justify their own project. Personally I prefer to use this over internal, mainly as I like to keep things open for reuse in most of projects.


### `/scripts`

Scripts to perform various build, install, analysis, etc operations.

These scripts keep the root level Makefile small and simple (e.g., [`https://github.com/hashicorp/terraform/blob/master/Makefile`](https://github.com/hashicorp/terraform/blob/master/Makefile)).

See the [`/scripts`](scripts/README.md) directory for examples.

### `/docs`

Design and user documents (in addition to your godoc generated documentation).

See the [`/docs`](docs/README.md) directory for examples.

### References
- [Standard Go Project Layout](https://github.com/golang-standards/project-layout)
- [Simple Go project layout with modules](https://eli.thegreenplace.net/2019/simple-go-project-layout-with-modules/)
- [`I'll take pkg over internal`](https://travisjeffery.com/b/2019/11/i-ll-take-pkg-over-internal/)
- [GopherCon EU 2018: Peter Bourgon - Best Practices for Industrial Programming](https://www.youtube.com/watch?v=PTE4VJIdHPg)
- [GopherCon 2018: Kat Zien - How Do You Structure Your Go Apps](https://www.youtube.com/watch?v=oL6JBUk6tj0)

### ToDo
- Differentiate between standard and library project layouts

## Private Registry


Optionale Umgebungsvariablen. Müssen entweder auf dem Hostsystem gesetzt sein, oder in der Console aus welcher VS Code gestarted wird exportiert worden sein!

REGISTRY_PATH 
HTTPS_PROXY
HTTP_PROXY
NO_PROXY

docker build --build-arg REGISTRY_PATH --build-arg  HTTPS_PROXY --build-arg HTTP_PROXY --build-arg NO_PROXY .
