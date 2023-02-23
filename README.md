# fly-yugabyte

Globally clustered [YugabyteDB](https://www.yugabyte.com/yugabytedb/) on [Fly.io](https://fly.io).

Built from <https://dev.to/yugabyte/yugabytedb-on-flyio-i-yugabyted-2eo7>

## How to Deploy

### 1. Create a YugabyteDB Fly App

```bash
fly launch my-yugabyte-db --no-deploy
```

### 2. Add Volumes

It can hav multiple per region, or multiple regions, or a mix of all:

```bash
fly volumes create yb_data --size 10 --region LAX -a my-yugabyte-db
fly volumes create yb_data --size 10 --region LAX -a my-yugabyte-db
fly volumes create yb_data --size 10 --region MIA -a my-yugabyte-db
fly volumes create yb_data --size 10 --region DEN -a my-yugabyte-db
```

This will make 2 instances in LAX, 1 in MIA, and 1 in DEN.

### 3. Deploy

```bash
fly deploy
```

Then scale out

```bash
flyctl scale count 4
```

### 4. Admin

Proxy the Yugabyte Tablet Dashboard & the direct postgres connection itself

```bash
flyctl proxy 27000:7000 &
flyctl proxy 25433:5433 &
```
