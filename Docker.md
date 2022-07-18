## Quick usage

Note:
- If you are still not ready for "Compose V2", try `docker-compose` instead of `docker compose` while we recommend upgrading Docker CLI
  See https://docs.docker.com/compose/#compose-v2-and-the-new-docker-compose-command

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

## docker on M1 Mac

- To build on M1 Mac, follow the steps below, skipping the `rake mrubyc_test` step to make it buildable.

```sh
docker compose build
docker compose run --rm prk rake setup
docker compose run --rm prk rake make_without_test
```

## Haste makes waste

After all, you may have to read [[Building-a-binary]] when you want to make things clear.
