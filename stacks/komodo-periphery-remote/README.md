# komodo-periphery-remote

Komodo-periphery-agent för **remote LXC-noder** (allt utom LXC 200 där
komodo-core själv kör med sin egen Local-periphery internt).

## Status

| LXC | IP | Använder denna stack |
|---|---|---|
| 203 | 192.168.68.103 | ✓ |

## Bootstrap (manuell deploy — inte Komodo-managed)

Den här stacken kan inte vara Komodo-managed eftersom den *ÄR* Komodos
periphery-agent på noden. Komodo kan inte deploya sig själv. Deploya
manuellt:

```bash
# På target-LXC:n (debian, med Docker installerat):
mkdir -p /opt/appdata/komodo-periphery
cd /opt/appdata/komodo-periphery
git clone --depth=1 git@github.com:Yicuqa/homelab.git /tmp/homelab
cp /tmp/homelab/stacks/komodo-periphery-remote/compose.yaml .
cp /tmp/homelab/stacks/komodo-periphery-remote/.env.example .env

# Sätt PERIPHERY_PASSKEY i .env (samma värde som Komodo-core använder)
$EDITOR .env

docker compose up -d
```

## Registrera i Komodo

Efter att periphery svarar på `http://<lxc-ip>:8120`:

1. Komodo UI → Servers → + New Server
2. Address: `http://<lxc-ip>:8120`
3. Save. Komodo-core autentiserar mot periphery med sin passkey.
