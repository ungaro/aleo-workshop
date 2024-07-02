# 1. Setup Environment

## Install Git and Rust

1. **Install [Git](https://git-scm.com/downloads)**
   - Follow the instructions on the Git website to download and install Git for your operating system.
2. **Install [Rust](https://www.rust-lang.org/tools/install)**
   - Follow the instructions on the Rust website to download and install Rust.

Note: After installation, if your `git` and `rustc` command don't work, try closing the current terminal window, opening a new one, and try again.

## Install leo

1. **Clone the `leo` repository:**

```bash
# Download the source code
git clone https://github.com/AleoHQ/leo
cd leo
git checkout testnet-beta
```

2. **Build and install the `leo` CLI:**

```bash
# Build and install
cargo install --path .
```

3. **Verify the installation:**

```bash
# To use leo
leo
```

For more details about how to use `leo` CLI, check out the [Leo Commands Guide.](https://developer.aleo.org/leo/commands)

## Install snarkOS

1. **Clone the `snarkOS` repository:**

```bash
git clone https://github.com/AleoHQ/snarkOS.git --depth 1
cd snarkOS
# Switch to the testnet3 branch
git checkout testnet-beta
```

2. **[For Ubuntu users] Run the helper script to install dependencies:**

```bash
./build_ubuntu.sh
```

3. **Install snarkOS**:

```
cargo install --path .
```

4. **Ensure ports are open**:

```
Make sure ports 4133/tcp and 3033/tcp are open on your router and OS firewall.
```

For more details about how to use `snarkOS` CLI, check out the [snarkOS Installation Guide.](https://developer.aleo.org/testnet/getting_started/installation/#22-installation).

Troubleshooting Common Issues with snarkOS
- Compiling Woes: Ensure Rust v1.66+ is installed and use ./run-client.sh or ./run-prover.sh to initiate snarkOS.
- Connectivity Issues: Check if ports 4133/tcp and 3033/tcp are open. Also, ensure you’ve used the right commands to start snarkOS.
- Address Generation Issues: Execute source ~/.bashrc before the snarkos account new command. Check your spelling; the directory is /snarkOS, but the command is snarkos.
- Please make sure you're installing snarkOS and leo from the testnet-beta branch.


## Install `leo` IDE Syntax Highlighting:

Follow the guide [here](https://developer.aleo.org/leo/installation#3-ide-syntax-highlighting) to set up syntax highlighting for Leo in your IDE.

## Docker pull leo

This is the development environment Docker image for the Aleo blockchain, which includes Leo, Rust, and Git installed.

Pull docker image

```
docker pull 0xaragondocker/leo_docker:latest
```

Run docker

```
docker run -it 0xaragondocker/leo_docker /bin/bash
```

## Windows Installation for Rust 

### Rust Installation
Rust runs on many platforms, and there are many ways to install Rust. This guide describes installation via rustup, a tool that manages multiple Rust toolchains in a consistent way across all platforms Rust supports. 
- On Windows, download and run [rustup-init.exe](https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe)
- rustup-init can be configured interactively, and all options can additionally be controlled by command-line arguments, which can be passed through the shell script. Pass --help to rustup-init as follows to display the arguments rustup-init accepts:
```
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --help
```
- The above command needs to executed using WSL
- If you prefer not to use the shell script, you may directly download rustup-init for windows [here](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe)
- verify rust installation by runnin ```rustc --version``` in wsl 

