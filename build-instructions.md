## Create the System Extension (extensions repo)

Since USB/IP modules don't exist in the stock kernel, the extension references
the custom kernel image that was built in the previous phase.

### Step 1 — Register and rebuild Makefile

Edit `.kres.yaml` in the extensions repo root and add `usbip` to targets:

```yaml
---
kind: pkgfile.Build
spec:
  targets:
    # ... existing targets ...
    - usbip
```

```bash
make rekres
```

### Step 2 — Build the extension

Point `PKGS` and `PKGS_PREFIX` to the custom kernel image that was built in the previous phase:

```bash
make usbip \
  REGISTRY=company.jfrog.io/ \
  PLATFORM=linux/amd64 \
  PKGS_PREFIX=company.jfrog.io/siderolabs \
  PKGS=v1.11.0-29-gaee690b-dirty \
  PUSH=true
```

Save the output:

```bash
export EXTENSION_IMAGE="company.jfrog.io/siderolabs/usbip:<tag>@sha256:<hash>"
```
