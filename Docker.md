## Quick usage

Note:
- If you are still not ready for "Compose V2", try `docker-compose` instead of `docker compose` while we recommend upgrading Docker CLI  
  See https://docs.docker.com/compose/#compose-v2-and-the-new-docker-compose-command
- As of May 2022, docker on M1 Mac doesn't work. Try building on the host instead  
  See [[Building a binary]]

### Setup

```sh
docker compose build
```

### Build

```sh
docker compose run --rm prk rake
```

#### Clean

```sh
docker compose run --rm prk rake clean
```

### Build with keymap (meishi2 for example)

```sh
git clone https://github.com/picoruby/prk_meishi2.git keyboards/prk_meishi2
docker compose run --rm prk rake build_with_keymap[prk_meishi2]
```

#### Clean

```sh
docker compose run --rm prk rake clean_with_keymap[prk_meishi2]
```

## Haste makes waste

After all, you may have to read [[Building-a-binary]] when you want to make things clear.
