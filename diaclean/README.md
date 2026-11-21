# DiaClean image build

`ghcr.io/diacleanshop/piler` = `sutoj/piler:<version>` + current Ubuntu security updates
(`apt-get upgrade`). Reason: the upstream image lags behind Ubuntu's PHP security backports
(PHP security release 2026-11-19, fixed in php8.5 `8.5.4-0ubuntu1.6`). The build fails if
`php8.5-fpm` is older than `MIN_PHP_DEB`.

Built by `.github/workflows/diaclean-image.yaml` on push to `diaclean/`, weekly and on demand.

Tags: `<version>-diaclean` (moving), `<version>-diaclean.<YYYYMMDD>` (pin this one), `sha-<commit>`.

Drop this once upstream releases an image with the fixed packages.
