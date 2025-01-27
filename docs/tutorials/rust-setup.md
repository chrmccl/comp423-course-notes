# Setting up a dev container for Rust

* Primary author: [Christopher McClanahan](https://github.com/chrmccl)
* Reviewer: [Jacob Dang](https://github.com/jacobdang207)

This tutorial will demonstrate how to set up a Rust Dev Container utilizing Visual Studio Code stored on a GitHub repository, and takes reference from [the MkDocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial) and the [Cargo documentation](https://doc.rust-lang.org/cargo/guide/creating-a-new-project.html).

# Prerequisites

Before setting up the DevContainer, make sure you have installed/created:

1. [Visual Studio Code](https://code.visualstudio.com/)
2. [Docker](https://www.docker.com/products/docker-desktop/)
3. [Git](https://git-scm.com/)
4. A [GitHub account](https://github.com/)

# Part 1. Creating the Git Repository

1. Open your terminal, and run the following command to create a new directory for your project and initialize a new git repository in it:
``` bash
mkdir "<directory-name-here>"
cd "<directory-name-here>"
git init
```

2. Create a `README.md` file and commit it:
``` bash
echo "# Rust Dev Container" > README.md
git add .
git commit -m "Initialize repository with README.md"
```

3. Create a [new GitHub repository](https://github.com/new); do not initialize it with a `README`, `.gitignore`, or license. Add the GitHub repository as the `origin` remote, and push the commit you created:
``` bash
git remote add origin https://github.com/<your-username>/<repository-name-here>
git push --set-upstream origin main
```

# Part 2. Setting Up the Dev Container

1. In VSCode, open the directory you created for the project. 

2. Install the **Dev Containers** extension for VSCode: press ++ctrl+shift+x++ to open the Extensions menu, search for and open the "Dev Containers" extension, and press the Install button.

3. Create a `.devcontainer` directory in the root directory of your project, and inside of it, create a `devcontainer.json` file with the following contents, and then re-open the project in the Dev Container by pressing ++ctrl+shift+p++ and typing then selecting "Dev Containers: Reopen in Container".
``` json
{
  "name": "Rust Hello World",
  "image": "mcr.microsoft.com/vscode/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  }
}
```

!!! Configuration

    In the `devcontainer.json` file, `image` tells VSCode to install a Microsoft-created image containing a Rust development environment, and `extensions` ensures that the `rust-analyzer` extension is automatically installed in VSCode.

# Part 3. Creating a New Project

1. First, check to make sure the Dev Container has installed a recent version of Rust: press ++ctrl+shift+grave++ to open a terminal, and run `rustc --version` to print the installed version of Rust. It should be the latest version, which as of now is `1.83.0`.

2. In order to create a new Rust project, run `cargo init --vcs none` in the root directory of your Dev Container. This will create a `Cargo.toml` file, which contains metadata and dependencies for your project, and a `src/main.rs` file, which will initially contain the following:
``` rust
fn main() {
    println!("Hello, world!");
}
```

3. If you want to change the name of your program, you can change the `name` field within `Cargo.toml`.

# Part 4. Creating a Basic Program

1. For our example, we will replace `"Hello, world!"` in `src/main.rs` with `"Hello COMP423"`, which should now contain:
``` rust
fn main() {
    println!("Hello COMP423");
}
```

2. In order to compile and run our program, we execute `cargo run`, this should output:
```
Hello COMP423
```

3. If we want to compile our program but not run it, we execute `cargo build`. This will build our project into an executable found under the `target/` directory. Compared to `cargo build`, `cargo run` will also run the target executable. In comparision with `gcc`, `cargo build` is to `rustc` as `make` is to `gcc`.

# Part 5. Commit and Push Our Changes

1. In order to commit and push our changes to GitHub, execute the following:
``` bash
git add .
git commit -m 'Create hello COMP423 program'
git push origin main
```
!!! Tip

    Since `cargo init` automatically creates a `.gitignore` file, we can stage our changes simply by running `git add .` without worrying about accidentially committing output files.

# Conclusion

