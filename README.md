# ruby-cloud-vision

This is a sample of Google Cloud Vision API.

## Before you begin

[Set up an API key](https://cloud.google.com/vision/docs/auth-template/cloud-api-auth?hl=ja#set_up_an_api_key)

## Requirement

* ruby
* bundler

## Install

```bash
git clone git@github.com:tmknom/ruby-cloud-vision.git && cd ruby-cloud-vision
bundle install --path=vendor/bundle
echo 'export GCP_API_KEY=[your_api_key]' >> .env
```

## Usage

```bash
# Display all tasks.
$ bundle exec rake -T

# Run face detection.
$ bundle exec rake vision:face[<path/to/image>]

# Compute a set of properties about the image (such as the image's dominant colors).
$ bundle exec rake vision:image_properties[<path/to/image>]

# Run label detection.
$ bundle exec rake vision:label[<path/to/image>]

# Run landmark detection.
$ bundle exec rake vision:landmark[<path/to/image>]

# Run logo detection.
$ bundle exec rake vision:logo[<path/to/image>]

# Run various computer vision models to compute image safe-search properties.
$ bundle exec rake vision:safe_search[<path/to/image>]

# Run OCR.
$ bundle exec rake vision:text[<path/to/image>]

# Unspecified feature type.
$ bundle exec rake vision:unspecified[<path/to/image>]
```

## License

MIT.

