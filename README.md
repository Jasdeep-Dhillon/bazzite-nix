# Bazzite Nix

A custom [bootc](https://github.com/bootc-dev/bootc) image template based on Bazzite with Nix package manager support. This image derives from `ghcr.io/ublue-os/bazzite-nvidia-open:stable` and adds terminal emulators and the Nix package manager.

## What's Included

- **Base**: Bazzite with NVIDIA open drivers (Universal Blue)
- **Additional Packages**: tmux, niri, kitty, ghostty
- **Nix Package Manager**: Pre-installed at `/nix`
- **Systemd**: podman.socket enabled by default

## Building

### Using Just

```bash
# Build the container image
just build

# Build a bootable QCOW2 virtual machine image
just build-qcow2

# Build a bootable ISO
just build-iso

# Build a bootable raw disk image
just build-raw
```

### Using Podman directly

```bash
podman build --tag bazzite-nix:latest .
```

### Running a VM

```bash
# Run a QCOW2 VM (builds automatically if needed)
just run-vm-qcow2

# Or with systemd-vmspawn
just spawn-vm
```

## Project Structure

```
bazzite-nix/
  Containerfile         # OCI image definition
  Justfile              # Build and management commands
  build_files/
    build.sh            # Package installation and customization script
  disk_config/
    disk.toml           # Bootc Image Builder config for disk images
    iso.toml            # Config for ISO builds
    iso-kde.toml        # Config for KDE ISO builds
    iso-gnome.toml      # Config for GNOME ISO builds
  .github/workflows/
    build.yml           # CI workflow for building OCI image
    build-disk.yml      # CI workflow for building disk images
```

## Customization

Edit `build_files/build.sh` to add or remove packages. The script uses `dnf5` and supports COPR repositories. The Containerfile can be modified to change the base image.

## Prerequisites

- A machine running a bootc image (Bazzite, Bluefin, Aurora, or Fedora Atomic)
- Podman or Docker for building images
- [just](https://just.systems/) command runner (included on Universal Blue images)
- GitHub account (for CI/CD workflows)

## Switching to Your Image

After building and pushing to a container registry:

```bash
sudo bootc switch ghcr.io/<username>/<image_name>
```

## Community

- [Universal Blue Forums](https://universal-blue.discourse.group/)
- [Universal Blue Discord](https://discord.gg/WEu6BdFEtp)
- [bootc Discussion Forums](https://github.com/bootc-dev/bootc/discussions)

## License

Apache-2.0
