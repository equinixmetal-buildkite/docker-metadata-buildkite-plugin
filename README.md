# docker-metadata

This Buildkite plugin applies a base set of tags and labels to Docker images, similar to the [GitHub CI Action](https://github.com/docker/metadata-action),

Results will be stored in a directory. The directory's path can be found in the `DOCKER_METADATA_DIR` environment variable.

Labels will be accessible through the `DOCKER_METADATA_DIR/labels` directory, while tags will be accessible through the `DOCKER_METADATA_DIR/tags` directory. To parse them, iterate over each file's lines.

## Example

Add the following to your `pipeline.yml`:

```yml
steps:
  - command: ls
    plugins:
      - equinixmetal-buildkite/docker-metadata#v1.0.0:
          images:
          - 'my-org/my-image'
```

The default settings will create a tag with the git commit SHA. (e.g. `my-org/my-image:12345678`).

Also, the image will be labeled with the following labels:

- `org.opencontainers.image.source=$BUILDKITE_REPO`
- `org.opencontainers.image.revision=$BUILDKITE_COMMIT`
- `org.opencontainers.image.created=<Current date in ISO 8601>`

## Configuration

### `images` (Required, array)

The image or set of images to build.

### `extra_tags` (Optional, array)

An extra set of tags to add to the image. E.g. `latest` or `dev`.

### `tag_prefix` (Optional, string)

Prefix all tags with provided string

### `title` (Optional, string)

The title of the image. This will be persisted as the `org.opencontainers.image.title` label.

### `licenses` (Optional, string)

The licenses of the image. This will be persisted as the `org.opencontainers.image.licenses` label.

### `vendor` (Optional, string)

The vendor of the image. This will be persisted as the `org.opencontainers.image.vendor` label.

### `debug` (Optional, boolean)

Enable debug logging for this plugin.

## Developing

To run the tests:

```bash
make test
```

## Contributing

1. Fork the repo
2. Make the changes
3. Run the tests
4. Commit and push your changes
5. Send a pull request
