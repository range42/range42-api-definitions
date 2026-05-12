# range42-api-definitions

OpenAPI specification for the CR42 backend API (`CR42 - API`, version `v0.1`).

---

## Contents

| File | Description |
|------|-------------|
| `openapi.json` | Machine-readable OpenAPI 3.x specification (used by Kong and tooling) |
| `openapi.json.pretty` | Human-readable formatted copy of the same spec |

---

## API Summary

**80 endpoints**, all under the `/v0/admin/` prefix.

| Route group | Endpoints | Description |
|-------------|-----------|-------------|
| `/v0/admin/proxmox/vms/` | 25 | VM lifecycle: create, clone, delete, start, stop, pause, resume, bulk operations, config queries |
| `/v0/admin/proxmox/vms/.../snapshot/` | 10 | Per-VM snapshot management: list, create, delete, revert |
| `/v0/admin/run/bundles/` | 30 | Run named bundles: Ubuntu package installs, user setup, Proxmox VM provisioning (admin / vuln / student roles) |
| `/v0/admin/run/scenarios/` | 1 | Run a named scenario by name |
| `/v0/admin/proxmox/firewall/` | 12 | Firewall rules and aliases at VM, node, and datacenter scope |
| `/v0/admin/proxmox/network/` | 6 | Network interface management on VMs and nodes |
| `/v0/admin/proxmox/storage/` | 4 | Storage listing, ISO listing, template listing, ISO download |
| `/v0/admin/debug/` | 2 | Health check (`ping`) and functional test (`func_test`) |

---

## How to Use

### Browse via Swagger UI

When the `range42-backend-api` service is running locally, the interactive Swagger UI is available at:

```
http://<backend-host>:<port>/docs
```

The raw OpenAPI JSON is served at:

```
http://<backend-host>:<port>/openapi.json
```

### Kong gateway bootstrap

Kong reads `openapi.json` to auto-configure its routes and upstream services. Point Kong's deck/sync configuration at this file to keep the gateway in sync with the current spec.

---

## Regenerating the Spec

The spec is generated directly from the running `range42-backend-api` application. From the root of that repo:

```bash
PYTHONPATH=. python -c "
import json
from app.main import create_app
print(json.dumps(create_app().openapi(), indent=2))
" > openapi.json
```

Then copy the result here and update `openapi.json.pretty` with the formatted version.

---

## Contributing

This is a collaborative initiative developed for applied security training, community integration, and internal capability building.
We use centralized community health files in the [Range42 community health](https://github.com/range42/.github) repository.

## License

GPL-3.0 — see [LICENSE](LICENSE).

