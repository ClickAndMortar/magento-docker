# Magento Docker

Magento / Adobe Commerce base Docker images for production usage.

## Available images

| Name                     | Version | PHP version | Dockerfile                              | Architectures    | Tags             |
|--------------------------|---------|-------------|-----------------------------------------|------------------|------------------|
| `clickandmortar/magento` | 2.4.7   | 8.3         | [Dockerfile](2.4.7/bookworm/Dockerfile) | `amd64`, `arm64` | `2.4.7-bookworm` |

## Usage

### Configuration

The `MAGE_MODE` environment variable can be set to `developer`, `production` or `default` (default is `production`).

If you need to override PHP or FPM configuration, you can mount custom configuration files:

* `custom.ini` should be mounted at `/usr/local/etc/php/conf.d/99-custom.ini`
* `www.conf` should be mounted over `/usr/local/etc/php-fpm.d/www.conf`

### Docker Compose

```yaml
version: '3.7'
services:
  magento:
    image: clickandmortar/magento:2.4.7-bookworm
    volumes:
      - ./:/app/
```
